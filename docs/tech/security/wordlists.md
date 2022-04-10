---
layout: post
title: Wordlist counts
description: Wordlist counts
date: 2022-04-09
---

I don't remember what I needed this for, but here is a list of some of my preferred wordlists and the number of words inside.

### Web directory/file fuzzing:
```
/usr/share/wordlists/dirb/common.txt (950 words)
/usr/share/seclists/Discovery/Web-Content/RobotsDisallowed-Top1000.txt (1k words)
/usr/share/wordlists/dirb/big.txt (20k words)
/usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-small.txt (81k words)
/usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt (220k words)
/usr/share/wordlists/allthewords.txt (391k words - combines dirb/dirbuster lists)
/usr/share/wordlists/content_discovery_all.txt (373k words - jhaddix list)
```

### VHOST Fuzzing:
```
/usr/share/seclists/Discovery/DNS/deepmagic.com-prefixes-top500.txt (500 words)
/usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt (5k words)
/usr/share/seclists/Discovery/DNS/shubs-subdomains.txt (484k words)
/usr/share/seclists/Discovery/DNS/dns-Jhaddix.txt (2M words - all DNS lists)
```

### Passwords:
```
/usr/share/seclists/Passwords/darkc0de.txt (1.4M words)
/usr/share/wordlists/rockyou.txt (14M words)
```

### LFI:
```
/usr/share/seclists/Fuzzing/LFI/LFI-Jhaddix.txt
```