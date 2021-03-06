---
layout: post
title: rdesktop
description: rdesktop cheatsheet
date: 2022-04-09 
---

### Remote in, 70% screen size share drives
```
rdesktop -u <user> -p <password> \$ <IP address> -g 70%
```

### Simple Rdesktop
```
rdesktop <IP>
```

### Use Clipboard
```
rdesktop <IP address> -5 -K -r clipboard:CLIPBOARD
```

### Use Credentials
```
rdesktop <IP address> -5 -K -r clipboard:CLIPBOARD -u <user> -d <domain> -p <password>
```

### Use Credentials, Mount Disk, and Enable Clipboard w/larger resolution
```
rdesktop <ip address> -5 -K -r clipboard:CLIPBOARD -r disk:tmp=/root/Desktop -u <user> -d <domain> -p <password> -g 1200x1000
```