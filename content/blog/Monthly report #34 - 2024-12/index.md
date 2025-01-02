---
title: Monthly report n⁰34 - 2024-12
summary: "We're happy to announce the release of the Firefox extension for Colander. It streamlines the capture of web content. 
This month also delivered improvements to usability. These include a new VueJS HAR analysis tool and significant improvements to Colander's deployment process, enhancing security and simplifying migrations."
description: "Monthly report of the activities on the PiRogue Tool Suite project"
lead: "PiRogue tool suite (PTS) is an open-source tool suite that provides a comprehensive mobile forensics and digital investigation platform."
date: 2024-12-31
lastmod: 2024-12-31
draft: false
weight: 50
type: blog
outputs:
   - 'html'
   - 'email'
contributors: ["Esther Onfroy"]
categories: ['activity reports']
toc_enabled: true
toc_start_level: 2
toc_end_level: 2
toc_ordered: false
---

# Project overview
PiRogue Tool Suite (PTS) provides a platform combining analysis tools, knowledge management, incident response management and artifact management, which allows NGOs with limited resources to equip themselves at a low cost. The project consists of an open-source tool suite that provides a comprehensive mobile device forensics and digital investigation platform.

* Website: [pts-project.org](https://pts-project.org)
* Email: `hello [at] pts-project.org`
* GitHub: [Source code](https://github.com/PiRogueToolSuite) - [Roadmap](https://github.com/orgs/PiRogueToolSuite/projects/3/views/4)
* Get support: [Discord](https://discord.gg/qGX73GYNdp)
* Support us: [OpenCollective](https://opencollective.com/pts)

---

# 📢 Announcements
* The Firefox extension for Colander has been released 🎉. Install it, [capture web pages and organize them in Colander](/cookbooks/colander-acquisition-extension-capture-tab/).
* The next community meeting will happen on Jan. 31 at 2pm CET. 
* Fill in [the form](https://docs.google.com/forms/d/e/1FAIpQLScT-0cH8rwKMSEKO-WK-6ipoNKnhV5FdcIH-sGJXOE7et5eTg/viewform?usp=sf_link) to select the Android app for next month.

# 🎉 Impacts and results
The Colander Firefox extension has been released. It streamlines the workflow for capturing and indexing web content into Colander. It reduces manual steps and improves efficiency for users who frequently use web content artifacts during their investigations.

We've addressed an interface detection issue in the `pirogue-admin` package. The issue occurred during at install time when the bonding module is loaded, incorrectly selecting `bonding_masters` as the isolated network interface. PiRogue now correctly supports bound network interfaces.

# 📒 Activity report
You can find more details about the different activities in the [project roadmap](https://github.com/orgs/PiRogueToolSuite/projects/3/views/4).


## 📦 US3 - Interoperability
The project seeks to enhance interoperability by enabling the import and export of knowledge in industry-standard format. This includes batch importing of knowledge, data interchange in MISP format, and the support for user-defined templates to generate custom knowledge feeds. PTS users must have the freedom to move their data and findings from and to other tools such as [OpenCTI](https://docs.opencti.io/latest/) or [MISP](https://www.misp-project.org/).

### Overview of the different activities
* 🔁 Import and export cases
* 🔁 Import and export knowledge from/to MISP format
* 🔁 Support user-defined templates to generate custom feeds
* 🔁 Use HAR to store the decrypted network traffic


### Use HAR to store the decrypted network traffic
#### This month
We have published the source code of the [HAR analyzer (viewer)](https://github.com/PiRogueToolSuite/har-analyzer-vuejs/). This tool is currently undergoing active development and is not suitable for production use.

#### Next month
We will continue the development of the HAR analyzer. The objective is to release it as a standalone tool and a VueJS library.


## 📦 US4 - Evidence collection
Efforts will be directed towards the extraction and preservation of artifacts and evidence, particularly those extracted from online content and mobile devices. The system will automatically archive and index various forms of online content such as photos, videos, social media posts, and web pages. Additionally, the capability of saving a watermarked capture or recording of the victim’s phone screen will be added to the PiRogue. In the context of forensic analysis, it is crucial to not only collect potential evidence of a compromise but also collect its  context, such as the attack vector. As an example, retrieving and storing tweets was key in the [Citizen Lab investigation on Predator](https://citizenlab.ca/2023/10/predator-spyware-targets-us-eu-lawmakers-journalists/), retrieving and storing WhatsApp messages in the [Citizen Lab investigation on Tibetan groups being targeted](https://citizenlab.ca/2019/09/poison-carp-tibetan-groups-targeted-with-1-click-mobile-exploits/).

### Overview of the different activities
* ✅ Archive and index online content
* ✅ Take a watermarked capture/recording of the phone screen

### Archive and index online content
#### This month
Colander now includes all the necessary tools to receive, review and, convert dropped files into Artifacts.
Colander Companion web-extension has been [released](https://pts-project.org/colander-companion/). The extension is officially signed by Mozilla and available for Firefox on desktop, mobile, and tablet.
The tests with webkit-based browsers were successful. The extension is not published on official add-ons marketplaces.
The documentation now includes new cookbooks and pages to cover installation and usage of web content acquisition tools.

#### Next month
Colander Companion and all related features included to Colander are entering maintenance phase.


## 📦 US8 - Colander deployment and administration
In an effort to ease the deployment and administration of Colander servers, functionalities such as importing and exporting entire cases, one-click deployment, and backup and restore tooling and procedures will be implemented, to enhance the overall manageability of the system. We would like to make it easier for end-users to deploy Colander since the [deployment procedure described on GitHub](https://github.com/PiRogueToolSuite/colander?tab=readme-ov-file#production-environment) can be tricky to follow if one does not have the technical expertise to do so.

### Overview of the different activities
* 🔁 1-click deployment
* 🔁 Backup and restore tools

### 1-click deployment
#### This month
The deployment of Colander with Ansible is composed of multiple steps. The first deployment requires installing Debian 12 and setting up a Unix user `colander` on the target server. One important aspect of this task is to improve the overall security and observability of Colander. The playbook `install_docker.yml` installs Docker in the *rootless* mode. In anticipation of the work that will be carried out on the migration procedure of Colander, the entire configuration of the stack is generated and saved in a single file that can be encrypted with *Ansible Vault*. The system administrator can back up this file and reuse it later when migrating Colander from one server to another. The rest of the deployment does not require any special privileges. 
Although this work is still in progress, we have already published the initial playbooks on [GitHub](https://github.com/PiRogueToolSuite/colander-ansible).

#### Next month
We will continue to work on this.


## 📦 US100 - Documentation
Documenting the project is key in its usability. We are continuously documenting the different tools and features we develop and build new learning materials to facilitate skills development.

#### This month
The documentation now includes new cookbooks to cover the installation and usage of the *Colander Companion* Firefox extension.
* [Colander Companion setup on desktop](https://pts-project.org/cookbooks/colander-companion-setup/)
* [Colander Companion setup on mobile](https://pts-project.org/cookbooks/colander-companion-mobile-setup/)
* [Save web pages with Colander Companion](https://pts-project.org/cookbooks/colander-acquisition-extension-capture-tab/)
* [Artifact acquisition documentation](https://pts-project.org/docs/colander/artifact-acquisition/) covering:
  * How to use third parties tools (like Colander Companion) to collect evidences
  * How to sort out evidences and convert them into Colander artifacts

#### Next month
We will continue to improve the project documentation to accurately reflect ongoing changes and updates.


## 📦 US101 - Maintenance
We manufacture PiRogues to supply organizations, while taking care of its maintenance. We will include OS upgrades, improvement of the documentation and fixing bugs. Regarding Colander and Threatr, we maintain the public Colander server, upgrade dependencies, improve the documentation and fix bugs.

#### This month
Thanks to a report by the [Qurium](https://www.qurium.org/) team, we've been able to confirm and fix [an issue regarding interface detection](https://github.com/PiRogueToolSuite/pirogue-admin/issues/25) in `pirogue-admin` package, which shows up when performing the autodetection at install-time, when the `bonding` module is loaded. The issue resulted in selecting `bonding_masters` as the isolated network interface.
Because `bonding_masters` is a file, not a directory, it lacks a `uevent` and defaults to `DevType.ETHERNET`, causing the issue. While excluding this name is possible, other similar entries might exist, making a comprehensive list difficult to maintain. Therefore, we propose requiring a `type` entry in each `net_dir` (regardless of whether it's a symlink or directory, as type filtering is complex), as documented in `Documentation/ABI/testing/sysfs-class-net`.

The version `2.0.6` of the package `pirogue-admin` fixes this issue.

#### Next month
We will continue the maintenance of the tools and the Debian packages we maintain.


## 📦 US102 - Community and outreach
Given the success of events, webinars and demos with members of the civil society, NGOs and security researchers, we continue with our outreach plan. We organize trainings and demonstration sessions as well as creating spaces for the community to share feedback and request new features via our mailing list, GitHub issues or Discord server.
We analyze one Android app that has received the community's interest (ex COP28 app) per month. The application to be analyzed is chosen by the community. The analysis report is first privately shared with the community and one month later it is publicly released.

We organize monthly calls open to all members of the community to share project updates and get the community’s feedback.

#### This month
The PTS community meeting has been postponed to a later date, since it was originally planned during Christmas holidays. The publication of the next analysis report has been postponed for the same reason. January's community meeting will happen on Jan. 31 at 2pm CET.

To supplement the traditional [feedback form](https://forms.gle/Ajof3sfKGCeHEBSj8), we are scheduling meetings with each organization utilizing PTS. This approach aims to foster a more interactive and efficient feedback collection process, enabling us to better understand user needs and implement relevant improvements.
During the early adoption phase of PiRogue VPN, we directly supported early adopters in Asia and Latin America. It was crucial to assist them during this phase, as they are deploying PiRogue VPN across a diverse range of hosting providers that we hadn’t tested. This phase revealed that PiRogue VPN is incompatible with DigitalOcean.

#### Next month
We will continue with our recurring activities.
