---
title: Analysis of Turaco >=1.1
summary: "Turaco app demonstrates a blend of typical social network capability while relying heavily on third-party SDKs. This analysis does not reveal any malicious behaviors."
lead: ""
date: 2024-11-22
lastmod: 2024-11-22
draft: false
weight: 50
toc: true
contributors: ["Esther Onfroy"]
images: []
categories: ['analysis reports']
---

**Turaco** was a social network Android app in Central African Republic that provides users with various features such as sharing opinions, reading the news and chatting with friends.

## Android samples
We've analyzed the following version of the app `com.she.turaco`:

* `fd3db2cc5c8683429594d534ee683981b59b52a7`
    * version: 1.1 (2)
    * certificate: *Common Name: Turaco Turaco* (`44a6d67e721ec521566cf1eefeab578fb2f0a080`)
    * origin: website
    * [Pithus](https://beta.pithus.org/report/adb2cc53d14b71cdeaeff7e25bc49af0376b803cd1b26a1637af5f11c8b97005)

* `4eab7d2c0b7055b39fc69b54dba29aa41ea52855`
    * version: 1.12 (13)
    * certificate: *Common Name: Turaco Turaco* (`44a6d67e721ec521566cf1eefeab578fb2f0a080`)
    * origin: website
    * [Pithus](https://beta.pithus.org/report/9d5da87c03aa9e5e5d1a8b8445b3d5b2960877e5ba0f3761b126bf94766420e5) - [VirusTotal](https://www.virustotal.com/gui/file/9d5da87c03aa9e5e5d1a8b8445b3d5b2960877e5ba0f3761b126bf94766420e5/behavior)

* `58590dc430d215c538237f41e66d50fa22cd37ac`
    * version: 1.12 (13)
    * certificate: *Common Name: Android, Organizational Unit: Android, Organization: Google Inc., Locality: Mountain View, State/Province: California, Country: US* (`ef184d91be0f5901c3282ffc1ffe1a16b041be42`)
    * source: Google Play
    * [Pithus](https://beta.pithus.org/report/04d159284443805f9a7cd98447178235e8aff15aa169fea1788aa7c77e60cea3) - [VirusTotal](https://www.virustotal.com/gui/file/04d159284443805f9a7cd98447178235e8aff15aa169fea1788aa7c77e60cea3/behavior)

* `6dfc2b4cfbc9f96cae1368a367e75d917273d921`
    * version: 1.16 (17)
    * certificate: *Common Name: Android, Organizational Unit: Android, Organization: Google Inc., Locality: Mountain View, State/Province: California, Country: US* (`ef184d91be0f5901c3282ffc1ffe1a16b041be42`)
    * source: Google Play
    * [Pithus](https://beta.pithus.org/report/87746816dd08331b53e4d16abcf487676bf32ea5d42bc7ffcbd8398105ecf77b) - [VirusTotal](https://www.virustotal.com/gui/file/87746816dd08331b53e4d16abcf487676bf32ea5d42bc7ffcbd8398105ecf77b/behavior?)

### Timeline
* Nov. 25, 2021: generation of the Turaco certificate `44a6d67e721ec521566cf1eefeab578fb2f0a080`
* Nov. 30, 2021: generation of the Google Play certificate `ef184d91be0f5901c3282ffc1ffe1a16b041be42`
* Nov. 30, 2021: registration of `turaco.me` domain name
* Nov. 28, 2022: first submission on VT of the sample 1.12 from Google Play `58590dc430d215c538237f41e66d50fa22cd37ac`
* Nov. 28, 2022: first submission on VT of the sample 1.12 from Turaco `4eab7d2c0b7055b39fc69b54dba29aa41ea52855`
* Dec.  1, 2023: expiration of the latest TLS certificate issued for the domain `turaco.me`
* Oct.  8, 2024: first submission on VT of the sample 1.16 from Google Play `6dfc2b4cfbc9f96cae1368a367e75d917273d921`

## APK Analysis
### Identification of the sample origin
APKs from Turaco's website are signed with the certificate `44a6d67e721ec521566cf1eefeab578fb2f0a080` while APKs from Google Play are signed with the certificate `ef184d91be0f5901c3282ffc1ffe1a16b041be42`. The 2 APKs in version `1.12` are exactly the same from a binary standpoint (100% similarity) regardless their origin (Dexofuzzy hash: `6144:+K6ttXJkU+yNrzgrcfLlb/NLPgoS11DjXoGqQgfiG71aa0kqWzVFwpBOdMQkOPUJ:DGyukrQlpZ7PVFwXnJhAqn`).

### Dangerous permissions (Google classification)
The earliest version (1.1) requests 9 permissions including:

* `android.permission.READ_EXTERNAL_STORAGE`: allows the application to read from external storage
* `android.permission.WRITE_EXTERNAL_STORAGE`: allows the application to write to external storage

The version 1.12 introduces the permission `android.permission.RECORD_AUDIO`, probably to record voice messages.

None of the versions we've analyzed request permissions to gain access to:

* the SMS messages (`.READ_SMS`/`.SEND_SMS`)
* the IMEI and IMSI (`.READ_PHONE_STATE`)
* the location (`.ACCESS_COARSE_LOCATION`, `.ACCESS_FINE_LOCATION`)
* the calendar (`.READ_CALENDAR`)


### Observations
The way the app is designed to communicate with Turaco's server is defined in `com/she/data/api/TuracoService` but nothing malicious has been identified.

This app relies on 3rd-party SDKs, five of them are known for collecting personal data:

* Facebook Analytics
* Facebook Login
* Facebook Share
* Google CrashLytics
* Google Firebase Analytics

{{< figure src="img/sdks.png" caption="List of SDKs embedded into the application" class="d-block mx-auto shadow" >}}

## Data Collection and Transmission
### Behavior analysis
It's important to note this app uses the [Androidx app compatibility library](https://developer.android.com/jetpack/androidx/releases/appcompat?hl=en). The purpose of this library is to make applications compatible with older versions of Android. The integration of this library leads to a large number of false positives when analyzed with automatic static analysis tools such as [Quark engine](https://github.com/quark-engine/quark-engine). The reason comes from the fact that this library offers a glue between operating system APIs and the Android app by overriding numerous OS APIs such as the ones for reading the IMEI, IMSI, access the agenda, read the SMS messages, list installed apps, etc. 

As an example, the call graph below shows that only the *Android App Compat* library calls the location-related methods such as `getLatitude`. But, the code of *Android App Compat* is never called by the app, this is *dead code*.

{{< figure src="img/location.png" caption="Call graph to the location API" class="d-block mx-auto shadow" >}}

For the sake of comparison, a call from the app (`com.she.turaco`) to the method returning the country ISO code of the mobile carrier is shown in the graph below. This graph also shows the SDK of Facebook (`com.facebook`) and the SDK of Google Data Transport (`com.google.android.datatransport`) read the network operator name.

{{< figure src="img/network-info.png" caption="Call graph to cellular network information API" class="d-block mx-auto shadow" >}}

The app version 1.16 implements all the code necessary to record audio as shown in the graph below. Probably for recording voice messages.

{{< figure src="img/record-audio.png" caption="Call graph to the audio recording API" class="d-block mx-auto shadow" >}}


## Dynamic analysis
The app version 1.1 was dynamically analyzed with [PTS](https://pts-project.org) and the dynamic analysis has shown network communications to Facebook and Google Firebase only. No *dangerous* (as defined by Google) permissions have been requested. The analysis can't go further than the registration screen since the app requests for a phone number with the country code `+236`. 

No communication with `*.turaco.me` has been observed.

### Facebook SDK
Four data transmissions to Facebook Graph have been observed. Those transmissions include:

* Advertising ID: a unique user identifier assigned by the Google Play service to a mobile device for tracking purposes
* Date and time of the installation of the app, when the app is launched, etc.
* The model and various other properties of the mobile device
* The timezone and the language of the phone
* The name of the mobile operator, this confirms what shows the second graph included above

Find below an example of data transmission to Facebook Graph:
```json 
format=json&sdk=android&custom_events=[
  {
    "_eventName":"fb_mobile_activate_app",
    "_eventName_md5":"cb7[redacted]7b9",
    "_logTime":1730134282,
    "_ui":"SignInActivity",
    "_session_id":"229[redacted]b88",
    "fb_mobile_launch_source":"Unclassified",
    "fb_mobile_pckg_fp":"758[redacted]4e9",
    "fb_mobile_app_cert_hash":"RKb[redacted]oIA=\n"
  },
  {
    "_eventName":"fb_sdk_initialize",
    "_eventName_md5":"d47[redacted]178",
    "_logTime":1730134275,"_ui":"unknown",
    "share_lib_included":"1",
    "applinks_lib_included":"1",
    "gamingservices_lib_included":"1",
    "messenger_lib_included":"1",
    "login_lib_included":"1",
    "all_lib_included":"1",
    "core_lib_included":"1",
    "_inBackground":"1",
    "_implicitlyLogged":"1"
  }
]
&event=CUSTOM_APP_EVENTS&anon_id=XZ0[redacted]6e9
&advertiser_id=7de[redacted]d05&extinfo=[
  "a2",
  "com.she.turaco",2,"1.1",
  "10",
  "SM-G965F",
  "en_US",
  "GMT+01:00",
  "F SFR",1440,2792,"3.5",8,52,51,"Europe\/Paris"
]&application_package_name=com.she.turaco&
```

This data transmission was handled by the SDK Facebook itself as shown in the stacktrace below:
```text
"com.android.org.conscrypt.NativeCrypto",
"[...]",
"com.android.okhttp.internal.huc.HttpsURLConnectionImpl",
"com.facebook.GraphResponse$Companion",
"com.facebook.GraphRequest$Companion",
"com.facebook.GraphRequest",
"com.facebook.appevents.AppEventQueue",
"com.facebook.appevents.AppEventQueue$flush$1",
"java.util.concurrent.Executors$RunnableAdapter",
"[...]",
"java.lang.Thread"
```


## Conclusion
In conclusion, the **Turaco** app demonstrates a blend of typical social network capability while relying heavily on third-party SDKs, particularly from Facebook and Google. While no malicious behavior nor code was detected, the app integrates SDKs known for extensive data collection, transmitting user-related information such as device details, advertising IDs, and mobile operator names to external servers. This raises potential privacy concerns.

The presence of permissions such as `RECORD_AUDIO` in later versions aligns with added features like voice messages but highlights the importance of transparent user communication regarding data use. Despite these permissions, dynamic analysis revealed limited direct communication with the app's own domain (`*.turaco.me`) and no direct access to sensitive data such as SMS, location, or IMEI, which suggests a cautious approach to permissions.

The dependence on Facebook SDKs for analytics and interaction, coupled with the evidence of data transmissions to Facebook Graph, underscores the potential for significant user data tracking. Overall, **Turaco** appears to function within standard practices for social network apps.