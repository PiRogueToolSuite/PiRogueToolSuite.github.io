---
title: "Upload a file to a Colander case"
---

With your PiRogue connected to your Colander account, you can upload artifacts and files to your cases. To do so, use the following command to upload a file to th4e given Colander case:

```shell {title="Upload a file to Colander"}
pirogue-colander collect-artifact -c "[ID of the case in Colander]" [file to be uploaded]
```

Then, choose the type of artifact to be created in Colander. This command can be found in workspace *Collect > Artifacts* in Colander.

{{< details "ℹ️ Example of upload to Colander" >}}
{{< terminal 
prompt="pi@pirogue ➜" 
title="Example of upload to Colander"
cmd="pirogue-colander collect-artifact -c \"404afb288c\" drop/IMG_1.jpeg" 
>}}
Select the type of the artifact for the file drop/IMG_1.jpeg:
0 - Android backup image
1 - Android sample
2 - Backup image
3 - Binary file
4 - Cryptographic activity trace
5 - Document
6 - Email file
7 - Forensic dump
8 - HAR file
9 - Image
10 - iOS backup image
Enter the number corresponding to the type you want to use: 9
You have selected Image
01:29:48 PM INFO     [pirogue_colander_connector.collectors.artifact] Start the upload of drop/IMG_1.jpeg
  drop/IMG_1.jpeg - complete ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 100% 0:00:00 0:00:00
{{< /terminal >}}
{{< /details >}}
