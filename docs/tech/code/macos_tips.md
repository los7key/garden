---
layout: post
title: Mac OS Tips
description: Mac OS Tips
date: 2022-08-23
Last Updated: 
---
## Introduction
When I find myself searching for things more than once or twice I like to put them somewhere I can easily find them again rather than having to search for them constantly.  This is where I'll put snippets of useful code and other commands, at least for now.™ 

## Flush DNS
```
sudo dscacheutil -flushcache;sudo killall -HUP mDNSResponder
```

## Change the Admin password without the password
This assumes you've already tried to reset using Apple ID

1. Restart
2. Press and hold `cmd + R` to start in recovery mode
3. Click on `Utilities` from the menu bar
4. Click on `Terminal` in the drop down menu
5. In the terminal, type: `resetpassword` and press "Enter"
6. Follow instructions to reset password

## Factory Reset

1. Click on the `Apple Icon` (in the top left corner)
2. Click `Open System Preferences`
3. Select `Erase all contents and Settings`
4. Enter your password for the admin account
5. Click `OK`
6. Click `Erase all Contents and Settings`

## Test Network Quality Directly From Terminal
```
$ networkquality
==== SUMMARY ====
Upload capacity: 18.189 Mbps
Download capacity: 156.692 Mbps
Upload flows: 20
Download flows: 20
Responsiveness: Medium (235 RPM)
```

## Caffeinate
Keep Mac from sleeping for X seconds
```
$ caffeinate -u -t 15
```

## Add ability to Quit Finder
```
$ defaults write com.apple.finder QuitMenuItem -bool true 
$ killall Finder
```
After applying the settings there will be an option to quit Finder from the Finder menu itself or using `cmd + Q`

