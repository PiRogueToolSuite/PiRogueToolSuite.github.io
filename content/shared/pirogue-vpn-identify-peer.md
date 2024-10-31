---
title: "Keep track of Wireguard peers"
---

The Wireguard peers configured on your PiRogue are not named, a peer is identified by its ID only. If you want to associate a peer to an individual, you have to store this information separately, ideality not on your PiRogue. We suggest you keep track of the peers the following way:

| Date       | Peer ID | Peer IP address | Individual |
| -----------|:-------:|:---------------:|:-----------|
| 2024-10-23 |     `2` |      `10.8.0.2` |       John |
| 2024-10-23 |     `3` |      `10.8.0.3` |        Lea |
| 2024-10-27 |     `6` |      `10.8.0.9` |    Camilla |


{{< details "ℹ️ How to find the IP address of a peer" >}}
The IP address of a peer is specified in the configuration of each peer, it corresponds to the `Address`. It's specified using [CIDR](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing#CIDR_notation) notation, ignore the value after the `/`. 

In this example, we want to get the IP address of peer 2. 
{{< terminal 
prompt="pi@pirogue ➜" 
title="Example of getting the IP address of peer 2"
cmd="pirogue-admin-client vpn get-peer-config 2" 
>}}
[Interface]
Address = 10.8.0.2/24  <--- IP address of peer 2
PrivateKey = WLzm+auxiGXJJDf/74TsS4hnAU4mViJxR8XfpJUviW0=
DNS = 10.8.0.1

[Peer]
EndPoint = 51.159.150.9:51820
PublicKey = dQzDsS2BQPjNjI2PG4hGAQX7AQ2xhFZnuMvV2beLj30=
AllowedIPs = 0.0.0.0/0
PersistentKeepAlive = 20
{{< /terminal >}}
{{< /details >}}