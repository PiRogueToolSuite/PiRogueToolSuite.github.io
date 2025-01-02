---
title: "Get the name of the isolated network interface"
---

A PiRogue, regardless of its operating mode, has 2 network interfaces. One to get access to the Internet named *external interface* and one named *isolated interface* to connect the devices to. The name of these 2 interface can be found in the system configuration of PiRogue.

The name of the isolated network interface can be found with the command below by looking at the `ISOLATED_INTERFACE` property:

```shell {title="Get the name of the isolated network interface"}
pirogue-admin-client system get-configuration
```

{{< details "How to get the isolated network interface" >}}
In this example, the name of the isolated network interface is `wg0`.
{{< terminal 
prompt="pi@pirogue ➜" 
title="Example of getting the isolated network interface"
cmd="pirogue-admin-client system get-configuration" 
>}}
DASHBOARD_PASSWORD: [redacted]
ENABLE_DHCP: 'True'
ENABLE_PUBLIC_ACCESS: 'True'
EXTERNAL_ADDRESS: [redacted]
EXTERNAL_INTERFACE: ens2
EXTERNAL_NETWORKS: [redacted]/32
ISOLATED_ADDRESS: 10.8.0.1
ISOLATED_INTERFACE: wg0  <-- isolated interface
ISOLATED_NETWORK: 10.8.0.0/24
PUBLIC_CONTACT_EMAIL: [redacted]
PUBLIC_DOMAIN_NAME: [redacted]
PUBLIC_EXTERNAL_ADDRESS: [redacted]
SYSTEM_HOSTNAME: pirogue-vpn-1
SYSTEM_OPERATING_MODE: wireguard
WIFI_COUNTRY_CODE: FR
WIFI_PASSPHRASE: [redacted]
WIFI_SSID: PiRogue1
{{< /terminal >}}
{{< /details >}}

