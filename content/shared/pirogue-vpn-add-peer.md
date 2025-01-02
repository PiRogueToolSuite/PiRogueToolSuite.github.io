---
title: "Create a new Wireguard peer"
---

To create a new Wireguard peer allowing a device to connect to the VPN network of the PiRogue, use the following command:
```shell {title="Add a new Wireguard peer"}
pirogue-admin-client vpn add-peer
```

{{< details "Get the list of Wireguard peers" >}}
To get the list of already configured peers, use the command:
```shell {title="List the Wireguard peers"}
pirogue-admin-client vpn list-peers
```

Example:
{{< terminal 
prompt="pi@pirogue ➜" 
title="Example of list of Wireguard peers"
cmd="pirogue-admin-client vpn list-peers" 
>}}
- idx: 2
  private_key: oA3PBMH5yhBCIykx1odFPbnH+QKq18FBPmdPU1MrmEQ=
  public_key: hdlwEsh7SQ0lEPC5Qpl66y9slJkhH4wUYEpzvkEq6V4=
- idx: 3
  private_key: YGe5EF//sIj6QF/2sglmx20b7jxgxFpV1sl8hXBDy34=
  public_key: 8lSksu3/HF8vCGi5lCOktI3C9L68PsfNhzDwyuAtMQ0=
{{< /terminal >}}
{{< /details >}}

{{< details "Delete a Wireguard peer" >}}
To delete a peer, you have to specify its index (`idx`):
```shell {title="Delete the peer #2"}
pirogue-admin-client vpn delete-peer [peer ID]
```
{{< /details >}}