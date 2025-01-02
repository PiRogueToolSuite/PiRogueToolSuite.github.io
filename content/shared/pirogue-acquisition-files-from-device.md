---
title: "Transfer files from a device to PiRogue"
---

If you want to retrieve files such as screenshots or log files from the device, you can start a file drop server allowing the user of the mobile device to upload files directly to your PiRogue. The mobile device must be connected to the isolated network of your PiRogue. 
To do so, run the following command on your PiRogue:
```shell {title="Start the file drop server"}
pirogue-file-drop -o [output folder]
```

The command starts a temporary web server accessible from the isolated network only. On the mobile device, open the webpage or scan the QR code and select the files you want to transfer.

Press `Enter` to stop the server. 

Once done, the output folder contains all the files and their metadata in `[file name].metadata.json`. The metadata files contain:
* `mimetype`: the type of the file such as image or video
* `modification_date`: the date of the last modification of the file before its transfer
* `modification_timestamp`: the timestamp of the last modification of the file before its transfer
* `original_filename`: the original name of the file before its transfer

{{< details "Transfer files from a device to PiRogue" >}}
In this example, we store the files in the folder `drop`.
{{< terminal 
prompt="pi@pirogue ➜" 
title="Example of file transfer to PiRogue"
cmd="pirogue-file-drop -o drop" 
>}}
 * Serving Flask app 'pirogue_evidence_collector.drop_server.server'
 * Debug mode: off
11:12:15 INFO     Flash the QR code on the mobile device or browse http://10.8.0.1:8080                            
                             
  █▀▀▀▀▀█ ▄█ ▄▄ ▀▄  █▀▀▀▀▀█  
  █ ███ █ ▄█▀█ ▄ ▀▄ █ ███ █  
  █ ▀▀▀ █ ▄ █ ▀▀▀▄  █ ▀▀▀ █  
  ▀▀▀▀▀▀▀ ▀ ▀ █ ▀ ▀ ▀▀▀▀▀▀▀  
  █▀███ ▀█▀█▀ ▀▀▄ ▀▀ ▀ ▀ █   
  ██▀ ▄▄▀▄██▄█▀  █▀▀   ▀ ▀█  
  ██ ▀  ▀▄ ▀▄▀▄▄ ▀▀▄▀▀▀▄▀█▀  
  █ ▀ ▀▄▀ ██▀ ▄█▀▀▄ ▄▀ █ ▀█  
  ▀ ▀▀▀ ▀ ██  ▀ ▀▄█▀▀▀█▄█    
  █▀▀▀▀▀█ ▀▀ █▀ ▄▄█ ▀ ██▀▀█  
  █ ███ █ █▄█▀▄▄▄█▀▀███▀███  
  █ ▀▀▀ █ █▄█ ▄█▀▀▄▄ ▄▄▄▀ █  
  ▀▀▀▀▀▀▀ ▀ ▀ ▀ ▀▀   ▀▀▀▀▀▀  
                             
Press Enter to stop the server
11:15:38 INFO     File saved: drop/IMG_2353.jpeg                                                                   
         INFO     File saved: drop/IMG_2352.jpeg                                                                   
         INFO     File saved: drop/IMG_2351.jpeg   
{{< /terminal >}}
{{< /details >}}

If you want to upload these files to Colander, please refer to [this cookbook](/cookbooks/pirogue-acquisition-upload-file-colander/).


