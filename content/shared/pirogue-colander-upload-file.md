---
title: "Upload file or folder Colander"
---

With your PiRogue connected to your Colander account, you can upload artifacts and files to your cases. To do so, use the following command to upload a file or the content of a folder to the given Colander case:

```shell {title="Upload a file to Colander"}
pirogue-colander collect-artifact -c "[ID of the case in Colander]" [file or folder to be uploaded]
```

If the path you have specified is a file, the command uploads this file only. If the path is a folder, the command uploads all the files contained into this folder. The command doesn't upload the files ending with `.metadata.json` as they contain the attributes to pass to Colander.

When asked, choose the type of artifact to create in Colander. The workspace *Collect > Artifacts* in Colander gives you the command to run.

{{< details "Example of upload to Colander" >}}
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
