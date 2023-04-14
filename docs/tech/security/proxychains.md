---
layout: post
title: proxychains cheetsheet
description: Proxychains cheetsheet
date: 2022-04-09
Last Updated: 2023-04-13
---

### configure proxychains

edit `proxychains.conf`

`vi /etc/proxychains.conf` -- at the bottom you will see

### Create a dynamic ssh tunnel
```
ssh -D 127.0.0.1:8080 sean@192.168.31.251
```

### add proxy here ...
```
#socks4 10.1.1.246 80
#socks4 10.1.1.246 22
```

### defaults set to "tor"

`#socks4 127.0.0.1 9050`  <--under this line put 

`socks4 127.0.0.1 8080`  <--this will use port 8080

```
proxychains nmap -T5 --top-ports=20 -sT -Pn 10.1.1.236
```