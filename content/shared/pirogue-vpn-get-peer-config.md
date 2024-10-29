---
title: "Get the configuration of a Wireguard peer"
---

To connect a peer to the Wireguard VPN, you first need to get its configuration. The peer configuration is returned by the command. You have to specify the ID of the peer you have previously created:
```shell {title="Get the configuration of a peer"}
pirogue-admin-client vpn get-peer-configuration [peer ID]
```

{{< details "ℹ️ Example of peer configuration" >}}
{{< terminal 
prompt="pi@pirogue ➜" 
title="Example of peer configuration"
cmd="pirogue-admin-client vpn get-peer-configuration 3" 
>}}
[Interface]
Address = 10.8.0.3/24
PrivateKey = YGe5EF//sIj6QF/2sglmx20b7jxgxFpV1sl8hXBDy34=
DNS = 10.8.0.1

[Peer]
EndPoint = 185.199.111.153:51820
PublicKey = YxtvfgfpgCpkQKTI9vcVz0LnXGHIwF83Z65OBWw4F0A=
AllowedIPs = 0.0.0.0/0
PersistentKeepAlive = 20
{{< /terminal >}}
{{< /details >}}

{{< details "ℹ️ Save the peer configuration in a file" >}}
To save the configuration of the peer in a `.conf` file to be loaded on the device, use the command: 
```shell {title="Save the configuration of the peer in a file"}
pirogue-admin-client vpn get-peer-configuration [peer ID] > my-peer-[peer ID].conf
```
{{< /details >}}