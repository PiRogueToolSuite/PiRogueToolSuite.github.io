---
title: "Get the configuration of PiRogue"
---

After the installation of the system, it's possible to get the current system configuration
with the following command:

```shell {title="Get the current system configuration"}
pirogue-admin-client system get-configuration
```

And check if everything is correct.

{{< details "ℹ️ Example of PiRogue configuration" >}}
{{< terminal 
prompt="pi@pirogue ➜" 
title="Example of configuration"
cmd="pirogue-admin-client system get-configuration" 
>}}
DASHBOARD_PASSWORD: PiRogue
ENABLE_DHCP: 'True'
ENABLE_PUBLIC_ACCESS: 'False'
EXTERNAL_ADDRESS: 192.168.1.37
EXTERNAL_INTERFACE: enp0s3
EXTERNAL_NETWORKS: 192.168.1.0/24
ISOLATED_ADDRESS: 10.8.0.1
ISOLATED_INTERFACE: wg0
ISOLATED_NETWORK: 10.8.0.0/24
PUBLIC_CONTACT_EMAIL: root@pirogue.local
PUBLIC_DOMAIN_NAME: pirogue.local
PUBLIC_EXTERNAL_ADDRESS: 185.199.111.153
SYSTEM_HOSTNAME: pirogue
SYSTEM_OPERATING_MODE: wireguard
WIFI_COUNTRY_CODE: FR
WIFI_PASSPHRASE: superlongkey
WIFI_SSID: PiRogue
{{< /terminal >}}
{{< /details >}}

