---
title: "Upload files from PiRogue to Colander"
description: "Upload files from PiRogue to Colander"
draft: false
toc: false
weight: 40
images: []
contributors: ["Esther Onfroy"]
params:
  steps: [
    "pirogue-colander-config",
    "pirogue-colander-upload-file",
  ]
type: 'cookbooks'
tags: ['pirogue', 'colander', 'upload', 'artifact']
categories: ['cookbooks']
group: 'f. Acquisition'
---

{{< callout context="caution" title="Requirements" icon="alert-triangle" >}}
* your PiRogue is up and running
* you have a Colander account 
{{< /callout >}}

{{< callout context="danger" title="Security considerations" icon="alert-octagon" >}}
Be cautious when transferring files:

* **Potential risks:** The files you want to transfer might contain malicious software or sensitive information.
* **No automatic protection:** Colander doesn't automatically scan or isolate these files.
* **Secure disposal:** Properly delete the files once you no longer need them.
{{< /callout >}}

{{< recipe >}}