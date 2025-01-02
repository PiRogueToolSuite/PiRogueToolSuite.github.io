---
title: "Time stamp files"
---

In some cases, it's crucial to [time stamp](https://en.wikipedia.org/wiki/Trusted_timestamping) collected files to securely keep track of the creation and modification time of a file. PiRogue uses an external timestamping authority. To do so, run the following command on your PiRogue:

```shell {title="Securely time stamp files"}
pirogue-timestamp -c [folder containing the files to time stamp]
```

The command generates a file `hashes.txt` listing the `sha512` hash of every files contained in the specified folder and generates the following files:
* `README.md`: the file containing the verification instructions
* `freetsa.org_cacert.*`: the certificate of the timestamping authority
* `hashes.txt`: the file listing the `sha512` hash of the timestamped files
* `hashes.txt.tsq`: the time stamp query
* `hashes.txt.tsr`: the time stamp reply


{{< details "Time stamp the content of a folder" >}}
In this example, we time stamp the files contained in the folder `drop`.
{{< terminal 
prompt="pi@pirogue ➜" 
title="Example of timestamping files"
cmd="pirogue-timestamp -c drop" 
>}}
15:47:26 INFO     Timestamping the files contained in drop                                                         
Using configuration from /usr/lib/ssl/openssl.cnf
{{< /terminal >}}
{{< /details >}}


