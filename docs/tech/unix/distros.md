---
layout: post
title: About Linux Distros
description: About Linux Distros
date: 2022-05-22
Last Updated: 
---
## Introduction

I recently saw a [Reddit](https://www.reddit.com) post[^1] from a user asking which [Linux](https://en.wikipedia.org/wiki/Linux) distribution is the best.  I started thinking about the first Linux box I set up many years ago.  I knew nothing about Linux and my good friend said if I wanted to learn, I need to start with [Slackware](http://www.slackware.com/).  I remember loading Slackware with [XFCE](https://www.xfce.org/) from a set of 3.5" disks[^2] what a chore it was.  I spent days installing the OS, compiling all the apps I needed, and even learning how to compile my own kernel. 

The interesting part about choosing a Linux distro is that you don’t have to change the OS to change the desktop environment (DE)[^3] and the window manager (WM)[^4] which will give the OS a completely different look and feel without having to install a different distro.  Many people new to Linux have a hard time grasping this idea since most people are generally used to MacOS or Windows where you have no choice.  Not only can you pick which one you want to use for Linux, but you can also install multiple DEs side by side and try different ones before you commit.  

Here are some DEs I really like:

* [XFCE](https://www.xfce.org/)
* [KDE](https://kde.org/)
* [Cinnamon](https://en.wikipedia.org/wiki/Cinnamon_(desktop_environment))
* [Gnome](https://www.gnome.org)

Here are some WMs I like:

* Enlightenment
* WIndowMaker 
* Compiz
* fvwm2

The best thing about Linux is even though you pick a DE and WM, you can still customize almost everything regarding look and feel.  It really depends on how much you want to tinker and how much time you have to fall down a deep rabbit hole.

Mostly, these days I just use a Mac as it just does what I need it to do without much tinkering.  When I’m in the mood to tinker or if I’m doing something that requires Linux I pretty much just run it in a VM.  The two distros I mostly use are [Mint](https://www.linuxmint.com/) with Cinnamon DE as my daily driver and [Kali](https://www.kali.org/) with XFCE for security-related projects.

I guess the tl;dr is the right distro for someone is really what they are comfortable with.  IMO, the big difference between distros is the package manager.[^5] So, the answer really is go with what you know for a daily driver.  You don't want to be searching for things or tinkering when you need to get something done. 

## Resources

* https://wiki.archlinux.org/title/Desktop_environment
* http://www.xwinman.org/

[^1]: Yes, I know that's not the actual post, but I couldn't find it again :(
[^2]: Keep in mind these disks held 1.44 megabytes (MB).  I think Slackware was only 5 or 6 disks around then, while Windows 3.1 was about a dozen.
[^3]: A desktop environment (DE) bundles together a variety of components to provide common graphical user interface elements such as icons, toolbars, wallpapers, and desktop widgets. Additionally, most desktop environments include a set of integrated applications and utilities. Most importantly, desktop environments provide their own window manager, which can however usually be replaced with another compatible one. 
[^4]: A window manager (WM) is system software that controls the placement and appearance of windows within a windowing system in a graphical user interface (GUI). It can be part of a desktop environment (DE) or be used standalone.
[^5]: A package manager is the tool used to install and maintain software packages.  For example, `apt` vs `rpm` vs `yum`.