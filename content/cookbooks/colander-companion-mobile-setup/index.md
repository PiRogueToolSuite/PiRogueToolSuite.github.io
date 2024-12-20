---
title: "Setup Colander Companion on mobile/tablet"
description: "Setup Colander Companion on mobile/tablet"
draft: true
toc: false
weight: 20
images: []
contributors: ["Christophe Andral"]
params:
  steps: [
    "colander-companion-get-api-colander-settings",
    "colander-companion-firefox-mobile-unlock-xpi-sideload",
    "colander-companion-download",
    "colander-companion-firefox-mobile-installation",
    "colander-companion-firefox-mobile-open-settings",
    "colander-companion-configure",
  ]
type: 'cookbooks'
categories: ['cookbooks']
group: 'f. Acquisition'
---

{{< callout context="caution" title="Requirements" icon="alert-triangle" >}}
* this assume you have installed Mozilla Firefox on your mobile/tablet device
{{< /callout >}}

Even though Colander Companion is validated and signed by Mozilla,
it is not publicly listed in the addons Mozilla extension store.
Unfortunately, Firefox Mobile does not automatically install trusted `.xpi` extensions
as the desktop version does.
That said, it is possible to enable this feature in your mobile browser.

{{< recipe >}}