---
title: ⌛ Beginner guide - How to handle a potentially malicious mobile app
weight: 30
toc: true
draft: false
---

On a daily basis, we encounter potentially malicious applications in various forms. They can appear as seemingly harmless apps we intend to download from Google Play (although it's rare -- Google usually takes them down), or they may be disguised as links or APK files shared within chat groups, especially if we are human rights defenders operating in a high-surveillance environment. Additionally, these malicious applications can be found on compromised devices.

In this guide, we will explore how to deal with applications, primarily focusing on Android applications, that raise suspicion of being potentially malicious.

Some Android malware masquerade as a normal application. Those files are called APKs (Android Application Package), and the very large majority of your Android applications are APKs.

{{< alert icon="👉" >}}
Because Google Play adds some information to most of the APKs when they are uploaded to the Play Store, it is possible to check for applications that come from it. This modification is called *frosting*. When you find an APK that is not frosted, you'd need to be extra careful with it. There are chances it is malicious.
{{< /alert >}}

In the next steps we will analyze a sample of a potentially malicious app and look for different indicators that can help us recognize a malicious app.

## Get the sample to be analyzed
First of all you need to get the sample for checking it. Malicious applications are commonly delivered through different types of channel:

* a link in a phishing email
* a link on chat groups
* a link on shady website
* on Google Play Store
* on alternative application stores

In some cases, the sample will have to be retrieved from a potentially compromised device. To do so, you can use [MVT](https://mvt.re) to [download the APK file from an Android phone](https://docs.mvt.re/en/latest/android/download_apks/).

If the application you want to analyze is available on Google Play Store, you can use [apkeep](https://github.com/EFForg/apkeep) to download it. Apkeep can be downloaded from [GitHub](https://github.com/EFForg/apkeep/releases/latest).

For this guide we will use an example sample that has been investigated before (fake Wire app) and available on Pithus. You can open and review the sample [here](https://beta.pithus.org/report/ae05bbd31820c566543addbb0ddc7b19b05be3c098d0f7aa658ab83d6f6cd5c8). 

To download the sample, follow [this link](/samples/sample_1.zip). You will get a ZIP archive protected by a password containing the sample APK. The password is `infected`.

## Compute the sample hash
After getting the sample you’ll need to securely store it, compute its [SHA256](https://en.wikipedia.org/wiki/SHA-2) hash and only work on copies of the original file. **This hash uniquely identify the sample file** based on its content. The SHA256 of two slightly different files will be totally different. SHA256 does not tell anything about how different the 2 files are. SHA256 (and other hashing functions) can be applied on any type of file.

It is advised to only work on copies of the original file and refrain from modifying it directly. A mobile application is essentially a zip archive that can be opened and unzipped. To initiate the reverse engineering process, you will need to open and modify a sample of the application. However, it is essential to ensure that you are working solely with copies of the original file. To accomplish this, store the original file, which you have received, in a designated folder on your computer. Alongside the file, store basic information about it, such as its SHA256 hash and package name. When you wish to perform in-depth analysis, create a duplicate of the file and commence working on this copy. Always remember to refrain from modifying the original file directly to preserve its integrity.

### Get the sample hash from Pithus
If you open the [Pithus report](https://beta.pithus.org/report/ae05bbd31820c566543addbb0ddc7b19b05be3c098d0f7aa658ab83d6f6cd5c8), you see in the *Fingerprints* workspace a section *File sums* specifying 3 different types of hash (MD5, SHA1 and SHA256). 

{{< img src="img/pithus_sha256.png" alt="SHA256 in Pithus" caption="SHA256 in Pithus" class="d-block mx-auto shadow md-5" >}}

### Compute the sample hash locally
You can compute the SHA256 of the sample directly on your computer with the following command line, replace `<my.apk>` my the path to the sample file:

| Operating system | Command                                                                |
|------------------|------------------------------------------------------------------------|
| on Linux         | `sha256sum <my.apk>`                                                   |
| on Windows       | `powershell: Get-FileHash .\<my.apk> -Algorithm SHA256 \| Format-List` |
| on Mac OS        | `shasum -a 256 <my.apk>`                                               |

The SHA256 of the sample we use in this guide is: `ae05bbd31820c566543addbb0ddc7b19b05be3c098d0f7aa658ab83d6f6cd5c8`

{{< alert icon="👉" >}}
When conducting reverse engineering on a mobile application, it is crucial to maintain the integrity of the original file.
{{< /alert >}}

{{< alert icon="👉" >}}
Always mention the sample hash (SHA256) in your report.
{{< /alert >}}

## Identify the type of sample
**APK or XAPK for Android**: a file with the `.apk` file extension is an Android Package file that's used to distribute applications on Google's Android operating system. APK files are saved in the ZIP format and are typically downloaded directly to Android devices, usually via the Google Play Store, but can also be found on other websites.

**IPA for iOS**: a file with the `.ipa` file extension is an iPhone application archive file which stores an iPhone app. It is usually encrypted with Apple's FairPlay DRM technology. Each `.ipa` file is compressed with a binary for the ARM architecture and can only be installed on an iPhone, iPod Touch, or iPad.

{{< alert icon="👉" >}}
Depending on your internal guidelines, you would have to digitally sign the sample with your PGP key for example.
{{< /alert >}}

## Retrieve basic information
Use tools to extract information that will help you identify the binary and its potential origin and behavior such as:

**Jadx**: is a software you can install on your computer to decompile Android application producing Java source code from Android Dex and APK files.

**Androguard**: is a software you can install on your computer to do reverse engineering and pentesting for Android applications.

**Pithus**: is an free and open-source online service that  statically analyze Android applications.

**VirusTotal**: is an online service that analyzes suspicious files and URLs to detect types of malware and malicious content using antivirus engines and website scanners.

{{< alert icon="👉" >}}
**Depending on your internal guidelines, never share your sample.** Depending on your internal guidelines, and depending on the confidentiality of the case you’re investigating, it would be not allowed to share the sample (or even the sample hash) on third party services like VirusTotal.
{{< /alert >}}

For this guide we will use two main tools to retrieve basic information for the example sample, Pithus and Jadx for exercising both options of analysis with online third party service and static offline analysis.

### With Pithus

#### Application name and package name
The application name is the name that will be displayed under the application icon on your phone. The package name is the technical name (identifier) of this application, the information that Android will be using to uniquely identify the application.

{{< img src="img/pithus_app_name.png" alt="Get both application and package names from Pithus" caption="Get both application and package names from Pithus" class="d-block mx-auto shadow md-5" >}}

#### Signing certificate information

The certificate plays a crucial role in distinguishing between the original application and potentially suspicious ones. Once you have obtained the application name and package name (as mentioned in the previous section), you can search for it on the Google Play Store and compare the signing certificate fingerprints. It's important to remember that the digital signature of Android applications cannot be faked. Two applications can have the same name, the same package name and have been signed with two different certificates. 

{{< img src="img/pithus_malicious_cert.png" alt="Signing certificate of the malicious sample" caption="Signing certificate of the <b>malicious sample</b>" class="d-block mx-auto shadow md-5" >}}

{{< img src="img/pithus_genuine_cert.png" alt="Signing certificate of the genuine Wire application" caption="Signing certificate of the <b>genuine Wire application</b>" class="d-block mx-auto shadow md-5" >}}

#### Google Play *frosting* information
To check if the sample was *frosted* by Google Play Store (Android only), refers to the *Frosting* information in the Pithus report.

{{< img src="img/pithus_malicious_frosting.png" alt="Frosting flag of the malicious sample" caption="Frosting flag of the <b>malicious sample</b>" class="d-block mx-auto shadow md-5" >}}

{{< img src="img/pithus_genuine_frosting.png" alt="Frosting flag of the genuine Wire application" caption="Frosting flag of the <b>genuine Wire application</b>" class="d-block mx-auto shadow md-5" >}}

#### Requested app permissions

Permissions can serve as an important indicator to determine whether an app is malicious or not. By reviewing the permissions requested, we can evaluate if they align with the legitimate purpose and functionality of the app. Take the example of the fake Wire app, which requests excessive permissions unrelated to its intended use as a communication app. This discrepancy raises suspicions about the app's integrity.

{{< img src="img/pithus_permissions.png" alt="Requested permissions by the malicious sample" caption="Requested permissions by the malicious sample" class="d-block mx-auto shadow md-5" >}}

