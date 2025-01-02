---
title: "Capture the network traffic with PiRogue VPN"
description: "Capture the network traffic with PiRogue VPN"
draft: false
toc: false
weight: 20
images: []
contributors: ["Esther Onfroy"]
params:
  steps: [
    "pirogue-config-isolated-interface",
    "pirogue-vpn-identify-peer",
    "pirogue-acquisition-network-traffic",
  ]
tags: ['pirogue', 'vpn', 'network_traffic']
type: 'cookbooks'
categories: ['cookbooks']
group: 'f. Acquisition'
---

{{< callout context="caution" title="Requirements" icon="alert-triangle" >}}
* your PiRogue VPN is up and running
* one or more devices are connected to it
{{< /callout >}}

{{< link-card
  icon="books"
  title="Learn how to capture network traffic"
  description="This guide will help you deepen your understanding of capturing network traffic."
  href="/guides/g2/"
>}}

{{< recipe >}}