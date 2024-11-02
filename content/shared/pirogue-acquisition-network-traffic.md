---
title: "Capture the network traffic"
---

With PiRogue, it's easy to capture the network traffic of all devices at once or the network traffic of a single device. 

#### Capture the whole network traffic
Simply use `tcpdump` and specify the name of the isolated interface:
```shell {title="Capture the whole network traffic"}
tcpdump -i [isolated interface] -w [PCAP file]
```
In the command above, replace 
* `[isolated interface]` with the name of the isolated interface
* `[PCAP file]` with the name of the file that will contain the network traffic

Press *Ctrl+C* to stop the capture.


#### Capture the network traffic of a single device
Use `tcpdump`, specify the name of the isolated interface and the IP address of the device:
```shell {title="Capture the network traffic of a device"}
tcpdump -i [isolated interface] host [device IP address] -w [PCAP file]
```
In the command above, replace:
* `[isolated interface]` with the name of the isolated interface
* `[device IP address]` with the IP address of the device whose traffic you want to capture
* `[PCAP file]` with the name of the file that will contain the network traffic

Press *Ctrl+C* to stop the capture.


{{< details "ℹ️ How to capture the network traffic of a device" >}}
In this example, the name of the isolated network interface is `wg0`, `10.8.0.2` is the IP address of the device and the network traffic will be saved in the file `/tmp/traffic.pcap`.
{{< terminal 
prompt="pi@pirogue ➜" 
title="Example of getting the isolated network interface"
cmd="tcpdump -i wg0 host 10.8.0.2 -w /tmp/traffic.pcap" 
>}}
tcpdump: listening on wg0, link-type RAW (Raw IP), snapshot length 262144 bytes
^C476 packets captured
476 packets received by filter
0 packets dropped by kernel
{{< /terminal >}}
{{< /details >}}

The PCAP file can be opened with Wireshark.
