---
layout: post
title: Dual Boot File Sharing 
description: Dual Boot File Sharing
date: 2022-07-08
Last Updated: 
---

Mount another partition so it's accessible from a dual boot host(linux/linux) with access control lists.

####  Make files world-accessible through an access control list 

```
$ sudo setfacl -m other:rwx -d -R .
$ sudo setfacl -m other:rwx -R .
```

#### Mount the filesystem 

```
$ sudo mount /dev/nvme0n1p6 /media/kali
$ bindfs -u bob /dev/nvme0n1p6 /media/kali
```

#### Get the files

```
$ cd /media/kali/home/kali/Documents

```

#### Add fstab entry

```
/dev/nvme0n1p6  /media/kali  auto  defaults  0 2
bindfs#/dev/nvme0n1p6  /media/kali  fuse  owner=bob
```
