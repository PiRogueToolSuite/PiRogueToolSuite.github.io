---
title: "Deploy PiRogue VPN"
---

Installation steps can be split into 2 phases: making sure the system is
up-to-date to start with (this isn't specific to the PiRogue ecosystem), then
configuring the PiRogue PPA and installing PiRogue packages.

```shell {title="Make sure the system is up-to-date"}
sudo apt-get update
sudo apt-get dist-upgrade
```

```shell {title="Configure the PiRogue PPA and install PiRogue packages"}
sudo apt-get install wget
sudo wget -O /etc/apt/sources.list.d/pirogue.list https://pts-project.org/debian-12/pirogue.list
sudo wget -O /etc/apt/trusted.gpg.d/pirogue.gpg   https://pts-project.org/debian-12/pirogue.gpg
sudo apt-get update
sudo apt-get install pirogue-base
```

During the installation, if prompted, you will have to answer:

- `Yes` to allow non-superusers to capture network traffic.

That's done! 