---
title: "Deploy PiRogue VPN"
description: "Deploy PiRogue VPN"
draft: false
toc: false
weight: 1
images: []
contributors: ["Esther Onfroy"]
params:
  steps: [
    "pirogue-vpn-deploy",
    "pirogue-get-configuration",
    "pirogue-public-access",
    "pirogue-dashboard-config",
  ]
type: 'cookbooks'
categories: ['cookbooks']
group: 'a. PiRogue VPN'
---

{{< callout context="caution" title="Requirements" icon="alert-triangle" >}}
* you already have a server accessible from the Internet
* your server has a public IP address
* your server runs Debian 12
* your server has at least 4GB of RAM and 40GB of disk

For more details, check [the installation](/docs/pirogue/installation/) and [the configuration](/docs/pirogue/version_2.x/configuration/) documentations.
{{< /callout >}}

{{< recipe >}}