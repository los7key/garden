---
layout: post
title: Cowrie Honeypot Setup
description: Cowrie Setup
date: 2022-07-30
Last Updated: 2022-08-13
---

## Set up host
```
sudo apt-get update
sudo apt-get install git python3-virtualenv libssl-dev libffi-dev build-essential libpython3-dev python3-minimal authbind

sudo adduser --disabled-password cowrie
sudo su - cowrie
```

## Set up cowrie
```
cd /home/cowrie/cowrie
virtualenv --python=python3 cowrie-env
source cowrie-env/bin/activate
(cowrie-env) $ pip install --upgrade pip
(cowrie-env) $ pip install --upgrade -r requirements.txt
```

## Modify cowrie configs 
```
cp /home/cowrie/cowrie/etc/cowrie.cfg.dist /home/cowrie/cowrie/etc/cowrie.cfg <-- Main cowrie config
cp /home/cowrie/cowrie/etc/userdb.example /home/cowrie/cowrie/etc/userdb.txt <-- Allowed users config
```

### Changes to cowrie.cfg
```
hostname = PROD03
listen_endpoints = tcp:22:interface=0.0.0.0
```

## Set up SSH and modify configs to allow cowrie on port 22
```
sudo apt-get install authbind
sudo touch /etc/authbind/byport/22
sudo chown cowrie:cowrie /etc/authbind/byport/22
sudo chmod 770 /etc/authbind/byport/22

vi /etc/ssh/sshd_config  # Change to a higher port
service ssh restart
```

## Integrations

1. Integration with [VirusTotal](https://www.virustotal.com/) (For malware scanning):
    - Go to virustotal.com and create a free account to get API key
    - Edit cowrie.cfg
    - Restart cowrie
```
[output_virustotal]
enabled = true
api_key = <API KEY>
upload = True
debug = False
scan_file = True
scan_url = True
```
1. Integration with [ThreatJammer](https://threatjammer.com/) (For flagging suspicious IPs):
    - Go to threatjammer.com and create free account to get API key
    - Edit cowrie.cfg
    - Restart cowrie
```
[output_threatjammer]
enabled = true
bearer_token = <API KEY>
api_url=https://dublin.report.threatjammer.com/v1/ip
track_login = true
track_session = false
ttl = 86400
category = ABUSE
tags = COWRIE,LOGIN,SESSION
```
 
## Visualization (Splunk)
Splunk is better than Kippograph. Since Splunk has much better looking graphics, I'll use that this time

1. Download Splunk Enterprise (free)
2. Add data inputs
    - Settings -> Add Data
    - Create HTTP Event Collector (leave everything default)
3. Get token and configure cowrie.cfg
4. Create cowrie index
    - Settings -> Data -> Indexes
    - Create new index "cowrie" 
5. Point Data Input to HTTP Collector
    - Settings -> Data -> Data Inputs
    - Point Data Input at cowrie index
6. Configure cowrie and restart
7. Add Manuka Honeypot app for dashboards (Obtained from the [Step by step guide](https://medium.com/@galolbardes/learn-how-to-deploy-a-honeypot-and-visualise-its-data-step-by-step-ea3cd3f25822) below)
   

```
[output_splunk]
enabled = true
url = https://127.0.0.1:8088/services/collector/event <-- Do NOT change the port for the collector
token = <TOKEN FROM SPLUNK>
index = cowrie
sourcetype = cowrie
source = cowrie
```

## Secure Splunk
Splunk will listen on all interfaces by default.  To make it not look like as big a target, we want to only allow it to listen on 127.0.0.1 and then we will use port forwarding to reach the Splunk UI:

1. Set SPLUNK_BINDIP=127.0.0.1 in $splunk_home/etc/splunk-launch.conf so it will only bind to localhost.
2. Connect via SSH port forwarding and open Splunk in a browser by going to http://127.0.0.1:8000

```
ssh -L 8000:127.0.0.1:8000 -p 7331 root@serverIP
```

## Resources 
This guide is comprised of trials, errors and parts of other guides.  Resources are listed below.

- [Step by step guide](https://medium.com/@galolbardes/learn-how-to-deploy-a-honeypot-and-visualise-its-data-step-by-step-ea3cd3f25822) I followed this guide initially
- [Cowrie Docs](https://cowrie.readthedocs.io/en/latest/)
- [Cowrie Slack](https://www.cowrie.org/slack/) <--- Great help here
- [Splunk Docs for BINDIP](http://docs.splunk.com/Documentation/Splunk/4.3.2/Admin/BindSplunktoanIP)
