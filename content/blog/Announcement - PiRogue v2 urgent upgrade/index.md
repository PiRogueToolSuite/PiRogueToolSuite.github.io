---
title:  "⚠️ PiRogue v2 - SYSTEM UPGRADE REQUIRED ⚠️"
description: "⚠️ PiRogue v2 - SYSTEM UPGRADE REQUIRED ⚠️"
date: 2024-10-31
lastmod: 2024-10-31
summary: "You must upgrade your PiRogue as soon as possible."
draft: false
weight: 50
type: blog
outputs:
   - 'html'
   - 'email'
contributors: ["Esther Onfroy"]
featured: true
categories: ['announcements']
---

We released version 2 of PiRogue on October 24, 2024. If you have installed a PiRogue since that date, you **must** run the following commands on your PiRogue as soon as possible:

```shell
wget -O /etc/apt/sources.list.d/pirogue.list https://pts-project.org/debian-12/pirogue.list
apt update
apt dist-upgrade
```

The mistake we made forces the installation to download Debian packages from the development PPA instead of the production PPA. The development PPA must not be used in production. There is no short term security concerns but we strongly invite you to upgrade your PiRogue as soon as possible.

If you want to check if your PiRogue is affected, run the following command and make sure it produces the exact same output as the one below:

{{< terminal 
prompt="pi@pirogue ➜" 
title="Check if you are using the production PPA"
cmd="cat /etc/apt/sources.list.d/pirogue.list" 
>}}
deb https://pts-project.org/debian-12/pirogue ./
deb https://pts-project.org/debian-12/pirogue-3rd-party ./
{{< /terminal >}}

If the output is not the same as above, contact us immediately on [Discord](https://discord.gg/qGX73GYNdp) or by email at `esther[at]defensive-lab.agency`.

We sincerely apologize for the inconvenience.
