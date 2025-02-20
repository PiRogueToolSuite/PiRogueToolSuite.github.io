---
title: "Deployment"
draft: false
images: []
menu:
  docs:
    parent: "colander"
weight: 506
toc: true
---

This guide walks you through deploying Colander on a dedicated server.

# Requirements
We recommend to use a dedicated server with at least:

* 4 cores
* 4GB of RAM
* 500GB of storage space

Your server must have a public IP address and run the latest version of Debian.

For the rest of this guide:
* 💻: indicates you must run the commands on your laptop ([Ansible control node](https://docs.ansible.com/ansible/latest/getting_started/basic_concepts.html#control-node))
* 📦: indicates you must run the commands on your server

You must run the commands starting with `ansible` on your laptop.

# Deployment procedure
The first step is to clone this repository on your laptop, not on the server. 
```shell {title="💻 Clone our playbooks on your laptop"}
git clone https://github.com/PiRogueToolSuite/colander-ansible.git
```

Regularly run the following command to update the playbooks:
```shell {title="💻 Pull new updates"}
git pull origin main
```


## Set up your server 
The latest version Debian must have been installed on your server before you start the deployment. 

Before running Ansible playbooks to install Colander, you must create a user `colander` on your server. Run the following commands on your server:
```shell {title="📦 Create a user colander on your server"}
useradd -m colander --shell /bin/bash
usermod -aG sudo colander
passwd colander
```


## Set up your laptop
To make things easier, we recommend copying the SSH key of the user `colander` on your server. 

On your laptop, run the command to copy it:
```shell {title="💻 Copy colander's SSH key on the server"}
ssh-copy-id -i ~/.ssh/my-key colander@[IP address of your server]
```

Then, on your laptop, create a Python 3 virtual environment and install the dependencies with the commands: 
```shell {title="💻 Set up the Ansible environment"}
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
ansible-galaxy install -r requirements.yml
```


## Inventory file
Your inventory file specifies the server on which Colander will be deployed. Rename the file `production-example.yml` to `production.yml` and replace:
* `[IP address of the server]` with the IP address of your server
* `[path of your SSH private key]` with the path of your SSH private key

Ansible will use the specified SSH key to connect to your server, this SSH key corresponds to the one you copied previously.

{{< details "Per host customization" >}}
If you want to customize (optional) what will be deployed, you can do it per host (server). To do so, in the folder `host_vars`, rename the file `production-example.yml` to `production.yml` in which you can override the default configuration. You can specify that you don't want to use:
* Threatr, by setting `use_threatr` to False
* Cyberchef, by setting `use_cyberchef` to False
* Mandolin, by setting `use_mandolin` to False
* Playwright, by setting `use_playwright` to False

You can also configure the amount of memory that will be allocated to Elasticsearch. See the example below.

Example of host configuration:
```yaml
stack_overrides:
  flavor:
    use_threatr: True
    use_cyberchef: False
    use_mandolin: False
    use_playwright: True
  services:
    elasticsearch:
      xms: 512m
      xmx: 512m
```
{{< /details >}}

## Install Docker
Then, it's necessary to install Docker on your server with the playbook `install-docker`:
```shell {title="💻 Install Docker on your server"}
ansible-playbook -K -i production.yml playbooks/install-docker.yml
```

Ansible will ask you to enter the *BECOME password* which corresponds to the password of the user *colander* you have created. The playbook installs Docker in the [rootless mode](https://docs.docker.com/engine/security/rootless/).


## Colander configuration
Before deploying Colander on your server, you must generate its configuration. The generated file contains all the secrets of your Colander server. Most of the secrets are randomly generated.

To generate the configuration, run the command on your laptop:
```shell {title="💻 Generate the configuration of Colander"}
ansible-playbook -i production.yml playbooks/generate-configuration.yml
```

The playbook will ask you to enter the root domain corresponding to your Colander server. Alternatively, you can pass it directly to the command line with: 
```shell {title="💻 Generate the configuration of Colander"}
ansible-playbook -i production.yml playbooks/generate-configuration.yml --extra-vars "root_domain=my.domain"
```

This creates a file `group_vars/colander/vault` in which you must specify:
* `acme_email`: the email address passed to Let's Encrypt
* `admin_name`: the server administrator’s full name
* `admin_email`: the email address the crash reports will be sent to
* `django_default_from_email`: the email address to use when sending emails
* `email_host`: the host of the SMTP server
* `email_host_user`: the username for the SMTP server
* `email_host_password`: the password for the SMTP server
* `email_port`: the port for the SMTP server
* `email_use_tls`: true if the SMTP server uses TLS, false otherwise
* `email_use_ssl`: true if the SMTP server uses SSL, false otherwise

Finally, back up and encrypt this file as it contains sensitive information and secrets:
```shell {title="💻 Encrypt the file that contains the secrets"}
ansible-vault encrypt group_vars/colander/vault
```

Don't forget to save the password of your vault in your favorite password manager.

⚠️ Before going further, make sure you have configured subdomains pointing to your server:
* `colander.[your domain]`
* `threatr.[your domain]` only if you are planning to deploy Threatr, check your inventory file
* `cyberchef.[your domain]` only if you are planning to deploy Cyberchef, check your inventory file
* `traefik.[your domain]`

As an example, if your domain is `my.domain` and the public IP address of your server is `253.127.98.9`, your A record would look like `colander.my.domain A 253.127.98.9`.

You are now ready to deploy Colander on your server 🎉


## Deploy Colander
You can now deploy Colander on your server. The playbook `colander` configures and deploys for you:
```shell {title="💻 Configure and deploy Colander"}
ansible-playbook -J -i production.yml playbooks/colander.yml
```

This is equivalent to running:
```shell {title="💻 Configure and deploy Colander in 2 steps"}
ansible-playbook -J -i production.yml playbooks/configure-colander.yml
ansible-playbook -J -i production.yml playbooks/deploy-colander.yml
```

Depending on your server, the first deployment can take several minutes to complete. The playbook automatically creates the `admin` users for Colander and Threatr (if enabled), and deploys the whole stack on your server.

Colander is now up and accessible on `https://colander.[root domain]/`.

Note that Colander is designed to update itself, but it doesn't update nor upgrade the server operating system.


# Maintenance
## Logs
The logs of the Docker containers are redirected to `journald` which is the standard logging service on Debian-based distributions. This allows seamless integration with external tools. As an example, `fail2ban` can be configured to ingest the logs of Colander and automatically block or ban IP addresses after `x` authentication failures.

The logs are tagged in a way that it’s easy to filter or extract them for a specific container, service, or type of service. As an example, the command 
```
journalctl -f CONTAINER_NAME=colander-colander-front-1  # 📦
``` 
prints the logs of the container `colander-colander-front-1`.

You can use the following variables to filter the logs:
* `IMAGE_NAME`: the name of the Docker image, *e.g.,* `ghcr.io/piroguetoolsuite/colander:main`
* `CONTAINER_NAME`: the name of the container, *e.g.,* `colander-colander-front-1`
* `COLANDER_SERVICE_NAME`: the name of the service, *e.g.,* `colander-front`
* `COLANDER_SERVICE_TYPE`: the type of service, *e.g.,* `web`

The values are defined in the Docker Compose file installed on the server.

### Authentication failures
All authentication failures are logged in `journald` with a fixed format:
`<date> <hostname> <container>: ERROR <date> signals 19 <timestamp> COLANDER_AUTH_FAILURE username:[<user>] email:[<email address>] ip:[<IP address of the client>] datetime:[<date>] routable:[<True if the IP address is public, False otherwise>]`

## Back up
A *bash* script is automatically installed in `/home/colander/colander/scripts`, when called, it creates:
* a dump of Colander database
* a dump of Threatr database (if deployed)
* a snapshot of Elasticsearch indices
* an archive containing all files stored in Minio

You can either run it on your server (`./scripts/backup`) or with Ansible on your laptop:
```shell {title="💻 Backup Colander"}
ansible-playbook -J -i production.yml playbooks/backup-colander.yml
```

The backups are stored in `/home/colander/colander/backups/` in a folder named with the date of the backup. The folder structure looks like this:
```
/home/colander/colander/backups/
`-- 2025_02_18-13_47_01
    |-- colander-db
    |   `-- backup_2025_02_18T13_47_02.sql.gz
    |-- elasticsearch
    |   `-- elasticsearch-2025_02_18-13_47_03.tgz
    |-- minio
    |   `-- minio-2025_02_18-13_47_03.tgz
    `-- threatr-db
        `-- backup_2025_02_18T13_47_03.sql.gz
```

You are free to use your favorite backup tool to schedule them according to your backup policies. We only provide the script to create the dumps and archives to be backed up.

Alternatively, you can create an archive of all Docker volumes after shutting down the whole stack. 


## Tear down Colander
If you want to completely uninstall Colander, run the playbook `teardown-colander.yml`. All containers, volumes, images, data, backups, configuration files will be permanently deleted. This action cannot be reverted.

```shell {title="💻 Tear down Colander"}
ansible-playbook -J -K -i production.yml playbooks/teardown-colander.yml
```

The playbook will ask you the password of the user `colander` and the password of your vault.

# Connect Colander to Threatr
To connect Colander to Threatr, follow these steps:
* In the Threatr administration panel, create a regular user in the menu *Users* menu and an API key for this user in the menu *Tokens*.

* In the administration panel of Colander, via the menu *Backend credentials*, create a new entry with `threatr` as backend identifier and for the credentials field, set 
```json
    {"api_key": "your Threatr API key"}
```

{{< callout context="note" title="Administration panel URLs" icon="info-circle" >}}
Note that the administration panels are accessible at random URLs:
* for Colander: `https://${colander_base_url}/${colander_django_admin_url}` with the variables set in your configuration vault
* for Threatr: `https://${threatr_base_url}/${threatr_django_admin_url}` with the variables set in your configuration vault
{{< /callout >}}

## Connect Threatr to 3rd-party vendors
In the Threatr administration panel, create new entries for the 3rd-party vendors in the *Vendor Credentials* menu.

{{< tabs "api_keys" >}}
  {{< tab "VirusTotal" >}}
  Use the vendor identifier `vt` and for the credentials field, set
  ```json
  {"api_key": "your API key"}
  ```
  {{< /tab >}}
  {{< tab "OTX Alien Vault" >}}
  Use the vendor identifier `otx` and for the credentials field, set
  ```json
  {"api_key": "your API key"}
  ```
  {{< /tab >}}
  {{< tab "Shodan" >}}
  Use the vendor identifier `shodan` and for the credentials field, set
  ```json
  {"api_key": "your API key"}
  ```
  {{< /tab >}}
  {{< tab "Scarlet Shark" >}}
  Use the vendor identifier `scarlet_shark` and for the credentials field, set
  ```json
  {"api_key": "your API key"}
  ```
  {{< /tab >}}
{{< /tabs >}}


{{< callout context="tip" title="Did you know?" icon="rocket" >}}
You can add multiple API keys for a same vendor, Threatr will do a round-robin on them. To do so, add multiple *Vendor Credentials* for the same vendor identifier.
{{< /callout >}}

# Development environment setup

Here's how to set up Colander for development:

Clone the Colander repository. Build and start the Colander stack using Docker Compose (or Podman). The `local.yml` provides the entire stack you need.

```bash {title="Setup the development environment"}
git clone https://github.com/PiRogueToolSuite/colander.git
cd colander
docker compose -f local.yml build 
docker compose -f local.yml up -d
docker compose -f local.yml run --rm django python manage.py createsuperuser 
docker compose -f local.yml logs -f -n 44 django  # to check the logs
```
Then, you should be able to access Colander at [http://localhost:8080](http://localhost:8080).

To stop the development environment, use:

```bash {title="Stop all services"}
docker compose -f local.yml stop
```
