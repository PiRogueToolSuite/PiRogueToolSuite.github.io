---
title: "Connect a mobile device"
description: "Connect a mobile device"
draft: false
toc: false
weight: 2
images: []
contributors: ["Esther Onfroy"]
params:
  steps: [
    "pirogue-vpn-add-peer",
    "pirogue-vpn-get-peer-config",
    "pirogue-vpn-connect-peer",
    "pirogue-vpn-identify-peer",
  ]
type: 'cookbooks'
categories: ['cookbooks']
group: 'a. PiRogue VPN'
---

{{< callout context="caution" title="Requirements" icon="alert-triangle" >}}
* you have already deployed a PiRogue online
* your PiRogue operates on the mode *Wireguard*
* the [Wireguard application](https://www.wireguard.com/install/) is already installed on the mobile device (Android or iOS)

🤔 Not done yet? Check the [documentation](/cookbooks/pirogue-vpn-installation/).
{{< /callout >}}

{{< callout context="danger" title="Security considerations" icon="alert-octagon" >}}
* **Remove VPN peer configurations:** Delete on the PiRogue and on peer's devices, any VPN peer configurations as soon as they're no longer needed.
* **Handle peer configurations with care:** Peer configurations contain sensitive information. Share them securely and privately.
* **PiRogue's IP address exposure:** Online services accessed through the VPN can see your PiRogue's IP address.
{{< /callout >}}


{{< recipe >}}