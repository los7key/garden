---
layout: post
title: Importing Kali VM Tweaks
description: Importing Kali VM Tweaks
date: 2022-07-17
Last Updated: 
---
I recently had to export a [Kali](https://www.kali.org/get-kali/) Linux VM from [vmware fusion](https://www.vmware.com/products/fusion/fusion-evaluation.html) on my Mac and import it on a Linux ([Mint](https://www.linuxmint.com/download.php) 20.3) machine.  There were a few hiccups along the way.  As usual, I took very few notes, but here are a few things that took a while to solve:

When importing be sure to click the actual image and not just the directory!

In Virtualbox App:

### Settings -> General
```
Name: vm (Doesn't matter)
Type: Linux
Version: Debian (64-bit) <-- This is not the default!
```
* This defaulted to Ubuntu and that was the final fix 

### Settings -> General -> Advanced
```
Shared Clipboard: Bidirectional <-- Disabled by default lol
Drag'n'Drop: Bidirectional <-- just in case
```

### Settings -> Display
```
Video Memory: 64 MB
Graphics Controller: VMSVGA <-- This was also not default
```

### Fix scrolling (on Kali host)
```
# apt install xinput
# xinput set-prop 'ETPS/2 Elantech Touchpad' 341 0
```