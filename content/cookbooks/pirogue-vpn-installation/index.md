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
tags: ['pirogue', 'vpn']
categories: ['cookbooks']
group: 'a. Setup'
---

{{< callout context="tip" title="Hosting providers compatibility" icon="rocket" >}}
* {{< inline-svg src="circle-check" stroke="#41C067" width="1.3rem" height="1.3rem" class="mb-1 svg-inline-custom" >}}Hetzner
  [{{< inline-svg src="external-link" width="1.0rem" height="1.0rem" class="mb-1 svg-inline-custom" >}}](https://www.hetzner.com/)
* {{< inline-svg src="circle-check" stroke="#41C067" width="1.3rem" height="1.3rem" class="mb-1 svg-inline-custom" >}}Scaleway
  [{{< inline-svg src="external-link" width="1.0rem" height="1.0rem" class="mb-1 svg-inline-custom" >}}](https://www.scaleway.com/)
* {{< inline-svg src="circle-x" stroke="#EE5080" width="1.3rem" height="1.3rem" class="mb-1 svg-inline-custom" >}}Digital Ocean (incompatible)
{{< /callout >}}

{{< callout context="caution" title="Requirements" icon="alert-triangle" >}}
* you already have a server accessible from the Internet
* your server has a public IP address
* your server has exactly 1 network interface
* your server runs Debian 12
* your server has at least 4GB of RAM and 40GB of disk

For more details, check [the installation](/docs/pirogue/installation/) and [the configuration](/docs/pirogue/version_2.x/configuration/) documentations.
{{< /callout >}}

{{< recipe >}}