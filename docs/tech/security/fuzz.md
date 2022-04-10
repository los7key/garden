---
layout: post
title: Fuzzing
description: Fuzzing with various apps
date: 2022-04-09
---
### ffuf fuzzing dirs
```
ffuf -c -e ".php,.txt,/" -w /usr/share/wordlists/allthewords.txt -u http://admirer.htb/admin-dir/FUZZ -t 75
-c color
-e extensions to fuzz (requires ".")
-w wordlist
-u url 
-t threads
```

### ffuf fuzzing vhosts
```
ffuf -c -w /usr/share/wordlists/dirb/common.txt -u http://quick.htb:9001 -H "Host: FUZZ" -mc 200 -fs 3351
-c color
-w wordlist
-u url 
-H Header to fuzz
-mc match code 200 only
-fs filter out size
```

### gobuster fuzzing dirs
```
$ gobuster dir -l -u http://backup.forwardslash.htb:80 -x php,html,txt -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt

dir - Directory/file brutceforcing mode
-l include length in response
-u URL
-x file types to search
-w wordlist
```

### gobuster fuzzing vhosts
```
$ gobuster vhost -u http://forwardslash.htb -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt

vhost - Vhost fuzzer
-u URL
-w wordlist
```

### wfuzz fuzzing vhosts

```
$ wfuzz -c -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -u "http://forwardslash.htb" -H "Host: FUZZ.forwardslash.htb" -t 30 --hh 0 
-c add color
-w wordlist
-u url
-H header (ex:"Cookie:id=1312321&user=FUZZ")
-t threads
--hh hide responses with 0 chars
```

### POST data

```
$ wfuzz -c -w "/usr/share/files" -d "password=FUZZ" -u "http://IP_ADDRESS" --hc 403,404 -t 42
-c Output text with colors nice feature.
-w wordlist
-d Post-Data (ex: "id=FUZZ&catalogue=1") 
-u url
--hc hide response codes 403 and 404
-t threads 
```

### POST data with PHP session data
```
$ wfuzz -c -b 'PHPSESSID=RepLAceME' -w '/the dictionary' -d 'http://Subscribe/to/ippsec.php?FUZZ=/etc/passwd'
-d post-data
--hh hide responses with a n(1,2,4,22) character length
-b Cookie or the php session id
-w Dictionary WordList 
-u url
```
