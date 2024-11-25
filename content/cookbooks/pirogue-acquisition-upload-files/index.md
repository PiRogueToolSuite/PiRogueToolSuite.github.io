---
title: "Transfer files from a device to PiRogue"
description: "Transfer files from a device to PiRogue"
draft: false
toc: false
weight: 3
images: []
contributors: ["Esther Onfroy"]
params:
  steps: [
    "pirogue-acquisition-files-from-device",
    "pirogue-acquisition-timestamp-files",
  ]
type: 'cookbooks'
categories: ['cookbooks']
group: 'f. Acquisition'
---

{{< callout context="caution" title="Requirements" icon="alert-triangle" >}}
* your PiRogue is up and running
* a device is connected to the isolated network
{{< /callout >}}

{{< callout context="danger" title="Security considerations" icon="alert-octagon" >}}
Be cautious with received files:

* **Potential risks:** The files you've received might contain malicious software or sensitive information.
* **No automatic protection:** PiRogue doesn't automatically scan or isolate these files.
* **Limit exposure:** Turn off the file drop server when you're done using it.
* **Secure disposal:** Properly delete the files once you no longer need them.
{{< /callout >}}

{{< recipe >}}