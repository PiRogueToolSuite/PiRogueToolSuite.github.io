---
title: Monthly report n⁰32 - 2024-10
description: "Monthly report of the activities on the PiRogue Tool Suite project"
lead: "PiRogue tool suite (PTS) is an open-source tool suite that provides a comprehensive mobile forensics and digital investigation platform."
summary: "We’re thrilled to announce the release of PiRogue v2, and it’s packed with powerful upgrades! 🎯 Get ready to experience a sleeker deployment, and new features that give you even more control over your PiRogue. Manage your PiRogue locally or remotely, deploy PiRogue on your local network or in the cloud, analyze network traffic of devices wherever they are on the globe."
date: 2024-10-27
lastmod: 2024-10-27
draft: false
weight: 50
type: blog
outputs:
   - 'html'
   - 'email'
contributors: ["Esther Onfroy"]
categories: ['activity reports']
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
* PiRogue v2 is here 🚀 more details in [the announcement](http://pts-project.org/blog/pirogue-v2-is-here-more-flexibility-more-control/). Test it, crash it, break it and share your feedbacks with us!
* The next community meeting will happen on Nov. 29 at 2pm CET. 
* The [analysis report](https://pts-project.org/blog/analysis-of-netguard-v2.330/) of NetGuard is now public.
* Fill in [the form](https://docs.google.com/forms/d/e/1FAIpQLScT-0cH8rwKMSEKO-WK-6ipoNKnhV5FdcIH-sGJXOE7et5eTg/viewform?usp=sf_link) to select the Android app for next month.

# 🎉 Impacts and results
**PiRogue v2 is here!** PiRogue now supports multiple operating modes including Wi-Fi access-point, appliance and VPN. Now, users can install their PiRogue at scale on, computers, virtual machines, bare-metal servers and VPS. PiRogue remains fully compatible with Raspberry Pi. This release represents a major step forward for PiRogue, offering greater flexibility. It can now be used to analyze the network traffic of a small organization by deploying it internally as a network appliance, or to capture and analyze the network traffic of a remote device through its VPN. Regardless the operating mode, the installation remains as simple as running a single command.

This new version of PiRogue has been by far the most difficult redesign we've had to carry out over the last three years. We are a very small team of 3 and it took us 3 months to implement it in 500+ changes, 8000+ lines of code, and 7 new Debian packages.


# 📒 Activity report

You can find more details about the different activities in the [project roadmap](https://github.com/orgs/PiRogueToolSuite/projects/3/views/4).



## 📦 US4 - Evidence collection
Efforts will be directed towards the extraction and preservation of artifacts and evidence, particularly those extracted from online content and mobile devices. The system will automatically archive and index various forms of online content such as photos, videos, social media posts, and web pages. Additionally, the capability of saving a watermarked capture or recording of the victim’s phone screen will be added to the PiRogue. In the context of forensic analysis, it is crucial to not only collect potential evidence of a compromise but also collect its  context, such as the attack vector. As an example, retrieving and storing tweets was key in the [Citizen Lab investigation on Predator](https://citizenlab.ca/2023/10/predator-spyware-targets-us-eu-lawmakers-journalists/), retrieving and storing WhatsApp messages in the [Citizen Lab investigation on Tibetan groups being targeted](https://citizenlab.ca/2019/09/poison-carp-tibetan-groups-targeted-with-1-click-mobile-exploits/).

### Overview of the different activities
* 🔁 Archive and index online content
* 🔁 Take a watermarked capture/recording of the phone screen



### Archive and index online content
#### This month
Welcome to **Colander Companion**, the first Colander browser extension.
As planned, this project relies on [SingleFile](https://github.com/gildas-lormeau/SingleFile) as an embedded third-party library. The alpha web-extension is in good shape as it now supports uploading collected content directly to Colander. The saved content is a snapshot of DOM of the webpage. This snapshot can be safely opened offline with any web browsers.
This extension gives users the option of automatically adding collected content directly to a Colander case. By default, all collected content is stored outside cases and must be sorted afterward.

#### Next month
We will add a new feature to this companion extension with the objective to invoke the download of the medias embedded into the saved webpage.

#### Challenges
Multiple security considerations and technical challenges were addressed to ensure a secure communication between the web extension and the Colander API.

### Take a watermarked capture/recording of the phone screen
#### This month
The first version of the `pirogue-evidence-collector` has been released, but it's not documented yet. This package is now installed by default on PiRogue and provides the user with the following commands:

* `pirogue-android` to interact with an Android device and run commands on it.
* `pirogue-file-drop` to expose a web server allowing the user to upload files from their device to the PiRogue. This command needs improvement. 
* `pirogue-extract-metadata` to extract metadata of a file and save it separately in `[original file name].metadata.json`.
* `pirogue-timestamp` to time stamp files by requesting a 3rd-party [RFC3161](https://www.ietf.org/rfc/rfc3161.txt) authority.
* `pirogue-intercept-[gated|single]` to instrument an Android application to analyze its network traffic. 

#### Next month
The implementation of the command `pirogue-file-drop` is not completed, as it needs to interact with the newly released administration tool to temporarily open a port on the isolated network. This integration will be done next month. Once all the commands are fully functional, we will publish the documentation.

#### Challenges
None.



## 📦 US9 - PiRogue virtualization
We want to provide end users with OS images and installation procedure allowing them to deploy PiRogue in a virtual environment (VM, cloud...). One of the direct implication is supporting a vast variety of configuration such as:
* Eth - Eth
* Wi-Fi - Eth
* VPN - Eth
* Wi-Fi - USB tethering

### Overview of the different activities
* ✅ ViRogue - Design and architecture
* ✅ ViRogue - Debian packaging
* ✅ ViRogue - Local and remote administration
* ✅ ViRogue - Tests
* ✅ ViRogue - Documentation



### ViRogue - Design and architecture
#### This month
The second major version of PiRogue has been released, the technical and architectural choices are detailed in the [system integration documentation](https://pts-project.org/docs/pirogue/version_2.x/system-integration/).

#### Next month
Nothing, as this task is now complete.

#### Challenges
None.

### ViRogue - Debian packaging
#### This month
All Debian packages have been bumped to version `2.x` and released. They are now available on our [PPA](https://github.com/PiRogueToolSuite/debian-12). Users can now migrade their PiRogues from `v1.x` to this new `2.x` version.

#### Next month
Nothing, as this task is now complete.

#### Challenges
None.



### ViRogue - Local and remote administration
#### This month
The PiRogue administration tool has been released. Extensive testing has been performed, from installation to fully functional remote administration. The tests cover all three new PiRogue operating modes.

#### Next month
Nothing, as this task is now complete.

#### Challenges
The wide variety of new PiRogue deployment scenarios was challenging to test from end-to-end. Automating VM environment creation and management would be a significant quality-of-life improvement for our testing efforts. 


### ViRogue - Tests
#### This month
Many tests were run, using laptops, mixing wired and wireless interfaces, and testing all desktop environments that can be selected from the Debian Installer. The VPN feature was also tested using a virtual machine hosted at Hetzner. Tests indicate that all supported modes of operation are functional.

#### Next month
Nothing, as this task is now complete.

#### Challenges
None.

### ViRogue - Documentation
#### This month
As we have released all the packages to virtualize PiRogue, the user documentation and the technical documentation have been published. This documentation covers:

* the [installation procedure](https://pts-project.org/docs/pirogue/installation/), detailing the different steps to be followed depending on the operating mode
* the [administration documentation](https://pts-project.org/docs/pirogue/version_2.x/configuration/), explaining how to configure and manage a PiRogue locally and remotely
* the documentation explaining the [technical choices](https://pts-project.org/docs/pirogue/version_2.x/system-integration/) we made for the system integration

#### Next month
Nothing, as this task is now complete.

#### Challenges
None.



## 📦 US100 - Documentation
Documenting the project is key in its usability. We are continuously documenting the different tools and features we develop and build new learning materials to facilitate skills development.

#### This month
We have updated the documentation of PiRogue to reflect all the changes that have been introduced with the release of the virtualization of PiRogue. We have also added details about the limitations of PiRogue when running on a Raspberry Pi such as low performance and the maximum of number of devices that can be connected to the PiRogue simultaneously.

Other edits were made to reflect minor project changes.

#### Next month
We will continue to improve the project documentation to accurately reflect ongoing changes and updates.

#### Challenges
None.



## 📦 US101 - Maintenance
We manufacture PiRogues to supply organizations, while taking care of its maintenance. We will include OS upgrades, improvement of the documentation and fixing bugs. Regarding Colander and Threatr, we maintain the public Colander server, upgrade dependencies, improve the documentation and fix bugs.

#### This month
A new version `v1.0.5` of [pcapng-utils](https://github.com/PiRogueToolSuite/pcapng-utils) has been released. And the package is now available on:
* our PPA as a Debian package
* [PyPi](https://pypi.org/project/pcapng-utils/) as a Python library

This new version supports 2 types of HAR enrichment:
* it adds the stacktrace associated with a network communication
* it replaces encrypted payloads with decrypted once

Find more details on [GitHub](https://github.com/PiRogueToolSuite/pcapng-utils).

We have improved the UX of the *Investigate* workspace of Colander, making its usage less confusing. A showstopper bug has been fixed in Colander as it was no longer possible to quickly create multiple entities at once. This bug was introduced when we reworked the *Investigate* workspace last month.

We have updated the Linux kernel for Raspberry Pi 5 to `v1:6.6.51-1+rpt2`.

#### Next month
We will continue the maintenance of all the tools and Debian packages we maintain.

#### Challenges
None.



## 📦 US102 - Community and outreach
Given the success of events, webinars and demos with members of the civil society, NGOs and security researchers, we continue with our outreach plan. We organize trainings and demonstration sessions as well as creating spaces for the community to share feedback and request new features via our mailing list, GitHub issues or Discord server.
We analyze one Android app that has received the community's interest (ex COP28 app) per month. The application to be analyzed is chosen by the community. The analysis report is first privately shared with the community and one month later it is publicly released.

We organize monthly calls open to all members of the community to share project updates and get the community’s feedback.

#### This month
We have publicly released the [analysis report](https://pts-project.org/blog/analysis-of-netguard-v2.330/) of the [NetGuard](https://play.google.com/store/apps/details?id=eu.faircode.netguard) Android application. 

The PTS community meeting took place on Oct. 25. This was a good opportunity to announce the second major release of PiRogue. The next community meeting will happen on Nov. 29 at 2pm CET. The release of the new version of PiRogue has been announced on our different communication channels such as Discord, mailing list and CiviCERT Mattermost. 

We're working on redesigning certain parts of the website, such as the home page, to present the project and its capabilities more effectively. This work includes providing short guides explaining how PTS can be used in different use cases, for example how to maintain detection rules with Colander or how to extract files from a mobile device with PiRogue. This work is part of a long-term effort to constantly improve the way we communicate about the project as it evolves.

We continue working on refining the way we collect user feedbacks on the usability of PTS, the way they use and the use cases they would like to see addressed in the future. 

#### Next month
We will continue with our recurring activities.

#### Challenges
None.



## 📦 US103 - Governance
#### This month
In order to strengthen the team, improve the organization of various project activities and follow up on potential partnerships currently under discussion, we are exploring the possibility of hiring a project coordinator. We are currently in the process of defining the scope of action and the various roles that the coordinator will have to fulfil.

In order to make the deployment and hosting of Colander and PiRogue easier, we are currently in discussion with several organizations to explore the different hosting modalities we could offer our users. These discussions are also intended to guide future developments of tools for system administrators to simplify the administration and maintenance of Colander and PiRogue servers.

#### Next month
We will continue with our recurring activities.

#### Challenges
None.



