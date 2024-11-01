---
title: "⬆️ PiRogue v2 - System Upgrade Recommended ⬆️"
description: "PiRogue v2 - System Upgrade Recommended"
date: 2024-10-31
lastmod: 2024-11-01
summary: "You should upgrade your PiRogue to ensure a correct configuration of the package manager."
draft: false
weight: 50
type: blog
outputs:
   - 'html'
   - 'email'
contributors: ["Esther Onfroy", "Cyril Brulebois"]
featured: false
categories: ['announcements']
# Stick to the original URL:
slug: "%EF%B8%8F-pirogue-v2-system-upgrade-required-%EF%B8%8F"
---

We released version 2 of PiRogue on October 24, 2024. If you installed a PiRogue between October 24, 2024 and October 31, 2024, the package manager's configuration might be incorrect. For affected systems, that means packages are downloaded from the development PPA instead of the production PPA.

We have deployed an updated `pirogue-base` package versioned `2.0.5`,  in both PPAs, that corrects this mistake automatically. Upgrading your system as usual should be sufficient to ensure a correct configuration:

```shell {title="Upgrade your PiRogue"}
sudo apt update
sudo apt dist-upgrade
```

After upgrading your system, you can compare the current configuration against the expected one.

- On all systems expect the Pi 5, you should get the following:

{{< terminal
prompt="pi@pirogue ➜"
title="Check if you are using the production PPA (all systems except Pi 5)"
cmd="cat /etc/apt/sources.list.d/pirogue.list"
>}}
deb https://pts-project.org/debian-12/pirogue ./
deb https://pts-project.org/debian-12/pirogue-3rd-party ./
{{< /terminal >}}

- On the Pi 5, you should get the following instead (note the extra, last line):

{{< terminal
prompt="pi@pirogue ➜"
title="Check if you are using the production PPA (Pi 5)"
cmd="cat /etc/apt/sources.list.d/pirogue.list"
>}}
deb https://pts-project.org/debian-12/pirogue ./
deb https://pts-project.org/debian-12/pirogue-3rd-party ./
deb https://pts-project.org/debian-12/pirogue-3rd-party-pi5 ./
{{< /terminal >}}

If the output is not the same as above, please contact us on [Discord](https://discord.gg/qGX73GYNdp) or by email at `esther[at]defensive-lab.agency`.

We sincerely apologize for the inconvenience.
