---
layout: post
title: Pi-Hole Notes
description: Pi-Hole Notes
date: 2022-08-01
Last Updated: 2023-02-18
---
### Upgrade to latest Raspbian 
Error:
```
E: Repository 'http://raspbian.raspberrypi.org/raspbian buster InRelease' changed its 'Suite' value from 'stable' to 'oldstable'
```

[Fix here](https://forums.raspberrypi.com/viewtopic.php?t=318302):
```
sudo apt-get update --allow-releaseinfo-change
```

Updating OS:
```
sudo apt update
sudo apt full-upgrade
```

Despite various sites saying it's not possible, I tried taking a shortcut and did a full upgrade instead of total install from scratch.  So far, so good, after 3 weeks.

Add `deb https://archive.raspberrypi.org/debian/ bullseye main` to /etc/apt/sources.list

### Reset Pi-Hole passwd
```
pi@gizmo:~ $ sudo pihole -a -p
Enter New Password (Blank for no password):
  [✓] Password Removed
```

### Update Pi-Hole
```
pi@gizmo:~ $ pihole -up
```

### Gravity-Sync 
(for replication)
I set this up years ago and pretty much just followed this guide.  There are 2 Pi-Holes and VIP that is used for DNS.  When one goes down, the other takes over at the VIP.

https://github.com/vmstan/gravity-sync


### Resources
* https://github.com/pi-hole/pi-hole

* https://docs.pi-hole.net/

