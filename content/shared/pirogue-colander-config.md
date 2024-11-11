---
title: "Connect your PiRogue to your Colander account"
---

You can connect your PiRogue to your Colander account and start collecting files and artifacts from it. To do so, in Colander, open your profile by clicking on your username and run the commands listed in your profile.

The command looks like:
```shell {title="Configure Colander on PiRogue"}
pirogue-colander config -u "[URL of Colander]" -k "[API key]"
```

{{< details "ℹ️ Example of Colander configuration command" >}}
{{< terminal 
prompt="pi@pirogue ➜" 
title="Example of Colander configuration on PiRogue"
cmd="pirogue-colander config -u \"https://colander.example.com\" -k \"47826e8163d4a5\"" 
>}}{{< /terminal >}}
{{< /details >}}
