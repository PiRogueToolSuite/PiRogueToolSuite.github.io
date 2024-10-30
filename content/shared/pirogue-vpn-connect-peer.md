---
title: "Connect the mobile device by scanning the QR-code"
---
Make sure the Wireguard application is already installed on the mobile device. 
Then, generate the QR-code and scan it with the Wireguard app:
```shell {title="Get the QR-code of a peer configuration"}
pirogue-admin-client vpn get-peer-config [peer ID] | qrencode -t ansiutf8
```