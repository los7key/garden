---
layout: post
title: Google Dorks
description: Google Dorks
date: 2023-05-13
Last Updated: 
---

## Introduction
Google dorks are special search terms that are used to access specific sets of information that are not usually available with normal queries.  This is really handy when looking for data on the web and is one of the best forms of <a href="/tech/musings/osint/" class="hvr-wobble-skew">OSINT</a>.

I was going to write a post on Google dorks including a cheat sheet and other useful information.  In doing some research I found some great cheat sheets already out there, along with really good information about it.  Rather than reinvent the wheel, I'll just include the links for cheatsheets I like and the dorks I use more frequently.

This is a WIP.

## Common Dorks  
* `site:` - Restrict search to this site/domain
* `allintext:` - Locate pages that contain certain characters or strings inside their text
* `allinurl:` - Fetch results whose URL contains all the specified characters
* `filetype:` - Search for any kind of file extension
* `allintitle:` - Show pages that contain titles with X characters
* `cache:` - Shows the cached version of a website

## Handy Examples
* `intitle:”index of” inurl:ftp` - Find open/exposed FTP servers
* `intitle:"index of" inurl:http after:2018` - Search for HTTP servers
* `filetype:xls inurl:"email.xls"` - Excel files that may contain email addresses
* `intitle:"Index of" wp-admin` - Find Wordpress admin pages
* `allintext:username filetype:log` - Find log files with "username" in the file
* `intitle:index.of id_rsa -id_rsa.pub` - Find SSH keys 
  
## Cheat Sheets
* <a href="https://www.exploit-db.com/google-hacking-database/" class="hvr-wobble-skew">ExploitDB</a> - A huge database of dorks and is searchable
* <a href="https://www.stationx.net/google-dorks-cheat-sheet/" class="hvr-wobble-skew">StationX</a> - Another great resource also searchable.
* <a href="https://book.hacktricks.xyz/generic-methodologies-and-resources/external-recon-methodology/github-leaked-secrets/" class="hvr-wobble-skew">HackTricks</a> - Security related dorks
