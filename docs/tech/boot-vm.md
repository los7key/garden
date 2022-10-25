---
layout: post
title: Boot VM from USB
description: Boot VM from USB
date: 2022-10-24
Last Updated: 2022-10-24
---
## Introduction
I needed to repartition a disk on a Linux VM and obviously the only way to do that is if the filesystem is read-only.  This means booting off a USB drive.  But how does the VM know to boot off the USB of the host?  This is how:

## Create the USB drive:
I created a USB boot disk for GParted Live
1. Get [GParted Live](https://gparted.org/livecd.php) iso
2. Create the image: `╰─$ sudo dd if=./gparted-live-1.4.0-5-amd64.iso of=/dev/sdb1 bs=4M; sync`

## Get the VM to boot off the USB drive
Boot VMware VM startup (gparted.live):

1. Power down VM
2. Virtual Machine -> Advanced
3. Change Firmware type to UEFI
4. Enable UEFI Secure Boot
5. Virtual Machine -> "Power on to Firmware" 
6. Select USB device

