---
layout: post
title: ModSecBox Honeypot Setup
description: ModSecBox Setup
date: 2023-04-23
Last Updated: 2023-04-23
---

## Introduction
As a learning opportunity I decided to set up <a href="/tech/security/cowrie_honeypot/" class="hvr-wobble-skew">another</a> honeypot.  What's the difference between this one and the previous iteration?  

It was a chance to review my notes from last time and I added a WAF component using <a href="https://github.com/SpiderLabs/ModSecurity/" class="hvr-wobble-skew">ModSecurity</a> running <a href="https://github.com/coreruleset/coreruleset" class="hvr-wobble-skew">OWASP’s Core Rule Set</a>. This is the OG defacto <a href="https://en.wikipedia.org/wiki/Web_application_firewall">Web Access Firewall (WAF)</a> that many firewalls (and appliances) are based on today.

I also built in on <a href="https://www.nginx.com/" class="hvr-wobble-skew">nginx</a> because it is different from <a href="https://httpd.apache.org/" class="hvr-wobble-skew">Apache HTTP Server</a> which is what I’m very familiar with.

To tie it all together the goal was to set up new dashboards and dive deeper into <a href="https://splunk.com" class="hvr-wobble-skew">Splunk</a> which is also the gold standard for visualizing data in an enterprise envirnonment.

There is some overlap with the <a href="/tech/security/cowrie_honeypot/" class="hvr-wobble-skew">setup of the previous</a> honeypot. While this walkthrough covers <a href="http://github.com/cowrie/cowrie" class="hvr-wobble-skew">cowrie</a> also, it is a bit more complete. 

## Stand up nginx
1. Install nginx
```
sudo apt update
sudo apt install nginx
```
2. Configure nginx
site-specific config files are kept in /etc/nginx/sites-available and symlinked into /etc/nginx/sites-enabled/
```
sudo unlink /etc/nginx/sites-enabled/default
sudo ln -s /etc/nginx/sites-available/example.com /etc/nginx/sites-enabled/
```
3. Test nginx
```
sudo nginx -t
sudo nginx -s reload
```
4. Start/Stop
```
sudo service nginx start
sudo service nginx stop
sudo service nginx restart
```

## Build ModSecurity

1. install dependencies
```
sudo apt install bison build-essential ca-certificates curl dh-autoreconf doxygen \
  flex gawk git iputils-ping libcurl4-gnutls-dev libexpat1-dev libgeoip-dev liblmdb-dev \
  libpcre3-dev libpcre++-dev libssl-dev libtool libxml2 libxml2-dev libyajl-dev locales \
  pkg-config wget zlib1g-dev libgd-dev git
```
2. Clone repo and cd
```
cd /opt && sudo git clone https://github.com/SpiderLabs/ModSecurity
cd ModSecurity
```
3. Initialize and update submodule
```
sudo git submodule init
sudo git submodule update
```
4. Compile
```
$ ./build.sh
$ ./configure
$ make
$ sudo make install
```

## Get ModSecurity-Nginx 
```
cd /opt && sudo git clone --depth 1 https://github.com/SpiderLabs/ModSecurity-nginx.git
```

## Building the ModSecurity Module For Nginx
1. Enumerate the version of Nginx
```
nginx -v

nginx version: nginx/1.22.0 (Ubuntu)
```

2. Download the exact version of Nginx running on your system into the /opt directory
```
cd /opt && sudo wget http://nginx.org/download/nginx-1.22.0.tar.gz
```

3. Extract the tarball
```
tar -zxvf nginx-1.22.0.tar.gz
```

4. Change to new directory
```
cd nginx-1.22.0
```

5. Display the configure arguments used for your version of Nginx
```
nginx -V
nginx version: nginx/1.22.0 (Ubuntu)
built with OpenSSL 3.0.5 5 Jul 2022
TLS SNI support enabled
configure arguments: --with-cc-opt='-g -O2 -ffile-prefix-map=/build/nginx-NEw8AJ/nginx-1.22.0=. -flto=auto -ffat-lto-objects -flto=auto -ffat-lto-objects -fstack-protector-strong -Wformat -Werror=format-security -fPIC -Wdate-time -D_FORTIFY_SOURCE=2' --with-ld-opt='-Wl,-Bsymbolic-functions -flto=auto -ffat-lto-objects -flto=auto -Wl,-z,relro -Wl,-z,now -fPIC' --prefix=/usr/share/nginx --conf-path=/etc/nginx/nginx.conf --http-log-path=/var/log/nginx/access.log --error-log-path=/var/log/nginx/error.log --lock-path=/var/lock/nginx.lock --pid-path=/run/nginx.pid --modules-path=/usr/lib/nginx/modules --http-client-body-temp-path=/var/lib/nginx/body --http-fastcgi-temp-path=/var/lib/nginx/fastcgi --http-proxy-temp-path=/var/lib/nginx/proxy --http-scgi-temp-path=/var/lib/nginx/scgi --http-uwsgi-temp-path=/var/lib/nginx/uwsgi --with-compat --with-debug --with-pcre-jit --with-http_ssl_module --with-http_stub_status_module --with-http_realip_module --with-http_auth_request_module --with-http_v2_module --with-http_dav_module --with-http_slice_module --with-threads --add-dynamic-module=/build/nginx-NEw8AJ/nginx-1.22.0/debian/modules/http-geoip2 --with-http_addition_module --with-http_gunzip_module --with-http_gzip_static_module --with-http_sub_module
```

6. The next step is to compile in Modsecurity module (apparently this is how it's done?).  You are supposed to copy all of the arguments following configure arguments: from your output of the above command and paste them in place of <Configure Arguments> in the following command.  However it didn’t like the geoip2 module that came with it, so I compiled in a new one.  Here is the configure command I used (includes modsec and geoip2):
```
./configure --add-dynamic-module=../ModSecurity-nginx --add-dynamic-module=../ngx_http_geoip2_module --with-cc-opt='-g -O2 -ffile-prefix-map=/build/nginx-NEw8AJ/nginx-1.22.0=. -flto=auto -ffat-lto-objects -flto=auto -ffat-lto-objects -fstack-protector-strong -Wformat -Werror=format-security -fPIC -Wdate-time -D_FORTIFY_SOURCE=2' --with-ld-opt='-Wl,-Bsymbolic-functions -flto=auto -ffat-lto-objects -flto=auto -Wl,-z,relro -Wl,-z,now -fPIC' --prefix=/usr/share/nginx --conf-path=/etc/nginx/nginx.conf --http-log-path=/var/log/nginx/access.log --error-log-path=/var/log/nginx/error.log --lock-path=/var/lock/nginx.lock --pid-path=/run/nginx.pid --modules-path=/usr/lib/nginx/modules --http-client-body-temp-path=/var/lib/nginx/body --http-fastcgi-temp-path=/var/lib/nginx/fastcgi --http-proxy-temp-path=/var/lib/nginx/proxy --http-scgi-temp-path=/var/lib/nginx/scgi --http-uwsgi-temp-path=/var/lib/nginx/uwsgi --with-compat --with-debug --with-pcre-jit --with-http_ssl_module --with-http_stub_status_module --with-http_realip_module --with-http_auth_request_module --with-http_v2_module --with-http_dav_module --with-http_slice_module --with-threads --with-http_addition_module --with-http_gunzip_module --with-http_gzip_static_module --with-http_sub_module
```

7. Build the modules with the following command:
```
sudo make modules
```
8. Create a directory for the Modsecurity module in your system's Nginx configuration folder:
```
sudo mkdir /etc/nginx/modules
```
9. Copy the compiled Modsecurity module into your Nginx configuration folder:
```
sudo cp objs/ngx_http_modsecurity_module.so objs/ngx_http_geoip2_module.so /etc/nginx/modules
```
10. Test config 
```
nginx -t

nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
```

11. Edit `/etc/nginx/ngix.conf` and insert:
```
load_module /etc/nginx/modules/ngx_http_modsecurity_module.so;
```

## Set up CRS
1. Clone repo 
``` 
sudo git clone https://github.com/coreruleset/coreruleset /usr/local/modsecurity-crs
```
2. Rename the crs-setup.conf.example to crs-setup.conf:
```
sudo mv /usr/local/modsecurity-crs/crs-setup.conf.example /usr/local/modsecurity-crs/crs-setup.conf
```
3. Rename the default request exclusion rule file:
```
sudo mv /usr/local/modsecurity-crs/rules/REQUEST-900-EXCLUSION-RULES-BEFORE-CRS.conf.example /usr/local/modsecurity-crs/rules/REQUEST-900-EXCLUSION-RULES-BEFORE-CRS.conf
```

## Configure Modsecurity
1. Create ModSecurity directory
```
sudo mkdir -p /etc/nginx/modsec
```
2. Copy over the unicode mapping file and the ModSecurity configuration file from your cloned ModSecurity GitHub repository:
```
sudo cp /opt/ModSecurity/unicode.mapping /etc/nginx/modsec
sudo cp /opt/ModSecurity/modsecurity.conf-recommended /etc/nginx/modsec/modsecurity.conf
```
3. Edit `/etc/nginx/modsec/modsecurity.conf` and change the value for `SecRuleEngine` to `On`
4. Create `main.conf` in `/etc/nginx/modsec` with the following lines
```
Include /etc/nginx/modsec/modsecurity.conf
Include /usr/local/modsecurity-crs/crs-setup.conf
Include /usr/local/modsecurity-crs/rules/*.conf
```

## Configure nginx
1. Edit `/etc/nginx/sites-available/default` to add:
```
modsecurity on;
modsecurity_rules_file /etc/nginx/modsec/main.conf;
```

## Set up Splunk 
1. Get Splunk (Free trial is good enough)
```
wget -O splunk-9.0.4.1-419ad9369127-Linux-x86_64.tgz "https://download.splunk.com/products/splunk/releases/9.0.4.1/linux/splunk-9.0.4.1-419ad9369127-Linux-x86_64.tgz"
```
2. Install Splunk
```
cd /opt
tar -zxvf splunk-7.2...
cd /opt/splunk/bin/
```
3. Secure Splunk
* Set `SPLUNK_BINDIP=127.0.0.1` in `$splunk_home/etc/splunk-launch.conf` so it will only bind to localhost.
* Connect via SSH port forwarding and open Splunk in a browser by going to `http://127.0.0.1:8000`
```
ssh -L 8000:127.0.0.1:8000 root@serverIP
```
4. Start Splunk
```
cd /opt && ./splunk start
```
5. Create collector
* Settings -> Add Data -> Monitor -> Files and Directories
```
Review
Input Type      Directory Monitor
Source Path     /var/log/nginx
Includelist     N/A
Excludelist     N/A
Source Type     Automatic
App Context     search
Host            modsecbox
Index           default
```
6. Create new index
* Settings -> Data -> Indexes
7. Confirm index is working
* New search with `index=*` will show that your index is being collected

## Installing cowrie 
See <a href="/tech/security/cowrie_honeypot/" class="hvr-wobble-skew">Cowrie Honeypot Setup</a>.