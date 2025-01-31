---
title: Analysis of MOI - Jordanian Ministry Of Interior v1.63
summary: "The analysis of MOI - Jordanian Ministry Of Interior v1.63 reveals that, despite requesting very sensitive information,it appears to be designed for a specific purpose and doesn't overuse complex SDKs to do what it is meant to do."
lead: ""
date: 2025-01-31
lastmod: 2025-01-31
draft: false
weight: 50
toc: true
contributors: ["Emy Canton"]
images: []
categories: ["analysis reports"]
---

---

**MOI - Jordanian Ministry Of Interior** is an Android application created by the Jordanian Ministry of interior, that provides users with information and services to request a visa, get the status of a visa request and annual residency services. The app requests sensitive information that are used to supply the Jordanian administration to create a visa request or renew an annual residency permit. These sensitive information don't appear to be sent to other services directly.
The analysis can’t go further than the registration screen since the account needs to be activated before continuing, no email were received, suggesting that it probably involves a human in the verification process of new account creations (which includes a passport picture verification).

Pithus report: https://beta.pithus.org/report/a00e4ad7c50106b9a7051581ad2863b6a8747271aa061bebef564b41fb38c075

## Android Sample

We’ve analyzed the following version of the app `com.moi.ministry.ministry_project`:

- MD5: `96f860a90dd09024a3b9edd86481d38b`
- SHA1: `e114c67fca7da5edf5376434771ce52275fb086d`
- SHA256: `a00e4ad7c50106b9a7051581ad2863b6a8747271aa061bebef564b41fb38c075`

## APK Analysis

### Application Info

- Package: `com.moi.ministry.ministry_project`
- Version name: `1.63`
- Version code: `63`

### Certificate Info

- MD5: `15771d1c2654eb042aee315883ee03e0`
- SHA1: `f90749781c97cfda7ea53af0d0f18b584b1a8d9b`
- SHA256: `7e250773a095d16fd141d4ba095ee58c94bf11549178ebe8cb7f0abb1766f762`
- Issuer: `Organization: Google Inc.`
- Not before: `2019-04-04T12:48:03+00:00`
- Not after: `2049-04-04T12:48:03+00:00`

### Dangerous permissions (Google classification)

This application requests the following permissions:

#### High risk

- `android.permission.WRITE_EXTERNAL_STORAGE`: Allows an application to write to external storage.
- `android.permission.READ_EXTERNAL_STORAGE`: Allows an application to read from external storage.
- `android.permission.CALL_PHONE`: Allows the application to call phone numbers without your intervention. Malicious applications may cause unexpected calls on your phone bill. Note that this does not allow the application to call emergency numbers.
- `android.permission.READ_PHONE_STATE`: Allows the application to access the phone features of the device. An application with this permission can determine the phone number and serial number of this phone, whether a call is active, the number that call is connected to and so on.

#### Medium risk

- `android.permission.MANAGE_DOCUMENTS`: Allows an application to manage access to documents, usually as part of a document picker.
- `com.google.android.c2dm.permission.RECEIVE`: Permission for cloud to device messaging.

#### Low risk & unclassified

- `android.permission.ACCESS_NETWORK_STATE`: Allows an application to view the status of all networks.
- `android.permission.ACCESS_WIFI_STATE`: Allows an application to view the information about the status of Wi-Fi.
- `android.permission.WAKE_LOCK`: Allows an application to prevent the phone from going to sleep.
- `android.permission.INTERNET`: Allows an application to access Internet.

- `android.permission.READ_MEDIA_IMAGES`: Allows an application to read image files from external storage.
- `android.permission.DOWNLOAD_WITHOUT_NOTIFICATION`: Allows the app to download files through the download manager without any notification being shown to the user.
- `android.permission.POST_NOTIFICATIONS`: Allows the application to post notifications.
- `com.google.android.gms.permission.AD_ID`
- `android.permission.ACCESS_ADSERVICES_ATTRIBUTION`
- `android.permission.ACCESS_ADSERVICES_AD_ID`
- `com.google.android.finsky.permission.BIND_GET_INSTALL_REFERRER_SERVICE`
- `com.moi.ministry.ministry_project.DYNAMIC_RECEIVER_NOT_EXPORTED_PERMISSION`

## Data Collection and Transmission

The app was dynamically analyzed with PTS and the dynamic analysis has shown network communications to eservice.moi.gov.jo and Google Firebase only.

### Google Firebase

The communication with Google Firebase is kept to the bare minimum with only the following data being transmitted:

```json
{
  "appId": "1:537131791653:android:67220efab816c9cf7196cc",
  "exp": 1738585184,
  "fid": "dxAC7p-bTceWP0pc41Dubf",
  "projectNumber": 537131791653
}
```

Along with the application version number, user language preference and locale.

```
1.63 29 en Europe/Paris
```

This data can be used to target advertisements and personalize content based on the user's geographic location

### Jordanian ministry

The account creation process requires the user to input a lot of **sensitive informations** such as: passport number, gender, first and last name, parents names, date of birth, nationalities, user's passport picture, etc...

```json
{
  "CaptchaCode": "WGH4PM",
  "CaptchaGUID": "2CF2BE71F9D75A52E06400144FF964BA",
  "InJordan": "0",
  "ProfileId": "",
  "NationalityCode": "311",
  "ForeignId": "",
  "Gender": "1",
  "MaritalStatus": "1",
  "PassSpouseName": "",
  "SpouseNationalityCode": "",
  "FirstName": "firstname",
  "FatherName": "fathername",
  "GrandName": "grandfathername",
  "FamilyName": "familyname",
  "PlaceOfBirth": "311",
  "DateOfBirth": "30-01-1995",
  "MotherNationality": "311",
  "MotherName": "mothername",
  "Investment": "0",
  "RegistrationNumber": "",
  "PartnershipShareAmpunt": "",
  "OrganizationName": "",
  "Capital": "",
  "Address": "",
  "PassportType": "2",
  "IdNumber": "0123456779",
  "IssueDate": "30-01-2017",
  "ExpiryDate": "30-01-2035",
  "IssuePlace": "311",
  "OtherPassportType": "",
  "Email": "test@example.com",
  "Username": "usernametest",
  "Password": "Test1234.",
  "ProfileAttachment": "<BASE64 PASSPORT PHOTO>",
  "MobileNumber": "0021234567890",
  "UserType": "1",
  "OriginalNationalityCode": "",
  "OriginalName": "",
  "OriginalFatherName": "",
  "OriginalGrandName": "",
  "OriginalFamilyName": "",
  "DocumentIssueCountry": ""
}
```

All this data is transmitted using HTTPS protocol with certificate pinning.

## Conclusion

The analysis of **MOI - Jordanian Ministry Of Interior v1.63** reveals a pretty straightforward application that seems to focus on only doing its job. While no malicious behavior nor code was detected, the app requires the user to supply very sensitive informations at account creation, with probable human verification of said information before validating said account creation.

The dangerous permissions asked are used to perform acceptable actions in the application. The `WRITE_EXTERNAL_STORAGE` permission is used to download administrative forms, the `READ_EXTERNAL_STORAGE` along with the `READ_MEDIA_IMAGES` permission is used to upload the required passport picture. The `CALL_PHONE` permission seems to be used to call the administration directly.

However, the presence of ad services permissions and the few network connections to Google's Firebase, along with the very sensitive personal data collected, may suggests that precise user tracking could be used after loging into a valid account.

Overall the application appears to be designed for a specific purpose and doesn't overuse complex SDKs to do what it is meant to do.
