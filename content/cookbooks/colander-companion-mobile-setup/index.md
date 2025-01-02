---
title: "Install Colander Companion on mobile/tablet"
description: "Install Colander Companion on mobile/tablet"
draft: false
toc: false
weight: 20
images: []
contributors: ["Christophe Andral"]
params:
  steps: [
    "colander-companion-firefox-mobile-unlock-xpi-sideload",
    "colander-companion-download",
    "colander-companion-firefox-mobile-installation",
    "colander-companion-firefox-mobile-open-settings",
    "colander-companion-configure",
  ]
type: 'cookbooks'
tags: ['colander_companion', 'extension']
categories: ['cookbooks']
group: 'a. Setup'
---

{{< callout context="caution" title="Requirements" icon="alert-triangle" >}}
You must have a Colander account.
{{< /callout >}}

Even though Colander Companion is validated and signed by Mozilla,
it's not publicly listed in the addons Mozilla extension store.
Unfortunately, Firefox Mobile doesn't automatically install trusted `.xpi` extensions
as the desktop version does.
That said, it's possible to enable this feature on your mobile browser.

{{< recipe >}}