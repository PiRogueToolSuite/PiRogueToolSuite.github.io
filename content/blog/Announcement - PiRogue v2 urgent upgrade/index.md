---
title: "⚠️ PiRogue v2 - SYSTEM UPGRADE REQUIRED ⚠️"
description: "PiRogue v2 - System Upgrade Required"
date: 2024-10-31
lastmod: 2024-10-31
summary: "You need to upgrade your PiRogue."
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

We released version 2 of PiRogue on October 24, 2024. If you installed a PiRogue between October 24, 2024 and October 31, 2024, you **must** run the following commands on your PiRogue:

```shell {title="Upgrade your PiRogue"}
sudo wget -O /etc/apt/sources.list.d/pirogue.list https://pts-project.org/debian-12/pirogue.list
sudo apt update
sudo apt dist-upgrade
```

The mistake we made forces the installation to download Debian packages from the development PPA instead of the production PPA. The development PPA must not be used in production. There is no short term security concerns but we strongly invite you to upgrade your PiRogue.

If you want to check if your PiRogue is affected, run the following command and make sure it produces the exact same output as the one below:

{{< terminal 
prompt="pi@pirogue ➜" 
title="Check if you are using the production PPA"
cmd="cat /etc/apt/sources.list.d/pirogue.list" 
>}}
deb https://pts-project.org/debian-12/pirogue ./
deb https://pts-project.org/debian-12/pirogue-3rd-party ./
{{< /terminal >}}

On Raspberry Pi 5, the line `deb https://pts-project.org/debian-12/pirogue-3rd-party-pi5 ./` must be present too.

If the output is not the same as above, contact us immediately on [Discord](https://discord.gg/qGX73GYNdp) or by email at `esther[at]defensive-lab.agency`.

We sincerely apologize for the inconvenience.
