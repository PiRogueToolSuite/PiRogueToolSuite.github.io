### Get the configuration of a Wireguard peer
To connect a peer to the Wireguard VPN, you first need to get its configuration. The peer configuration is returned by the command. You have to specify the ID of the peer you have previously created:
```shell {title="Get the configuration of the peer #3"}
pirogue-admin-client vpn get-peer-configuration 3
```
Then, you need to save the configuration of the peer in a `.conf` file to be loaded on the device. To do so, use the command: 
```shell {title="Save the configuration of the peer #3 in the file my-peer-3.conf"}
pirogue-admin-client vpn get-peer-configuration 3 > my-peer-3.conf
```

Alternatively, you can generate a QR-code to be scanned with the Wireguard mobile app:
```shell {title="Get the configuration of the peer #3 QR-code"}
pirogue-admin-client vpn get-peer-config 3 | qrencode -t ansiutf8
```