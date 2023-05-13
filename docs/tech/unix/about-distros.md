---
layout: post
title: About Linux Distros
description: About Linux Distros
date: 2022-05-22
Last Updated: 2023-05-13
---
## Introduction

I recently saw a <a href="https://www.reddit.com" class="hvr-wobble-skew">Reddit</a> post[^1] from a user asking which <a href="https://en.wikipedia.org/wiki/Linux" class="hvr-wobble-skew">Linux</a> distribution is the best.  I started thinking about the first Linux box I set up many years ago.  I knew nothing about Linux and my good friend said if I wanted to learn, I need to start with <a href="http://www.slackware.com/" class="hvr-wobble-skew">Slackware</a>.  It was definitely a learning experience!  I remember loading Slackware with <a href="https://www.xfce.org/" class="hvr-wobble-skew">XFCE</a> from a set of 3.5" disks[^2] and what a chore it was.  I spent days installing the OS, compiling all the apps I needed, and even learning how to compile my own kernel. 

The interesting part about choosing a Linux distro is that you don’t have to change the OS to change the desktop environment (DE)[^3] and the window manager (WM)[^4] which will give the OS a completely different look and feel without having to install a different distro.  Many people new to Linux have a hard time grasping this idea since most people are generally used to MacOS or Windows where you have no choice.  Not only can you pick which one you want to use for Linux, but you can also install multiple DEs side by side and try different ones before you commit.  

Here are some DEs I really like:

* <a href="https://www.xfce.org/" class="hvr-wobble-skew">XFCE</a>
* <a href="https://kde.org/" class="hvr-wobble-skew">KDE</a>
* <a href="https://en.wikipedia.org/wiki/Cinnamon_(desktop_environment)" class="hvr-wobble-skew">Cinnamon</a>
* <a href="https://www.gnome.org" class="hvr-wobble-skew">Gnome</a>

Here are some WMs I like:

* Enlightenment
* WIndowMaker 
* Compiz
* fvwm2

The best thing about Linux is even though you pick a DE and WM, you can still customize almost everything regarding look and feel.  It really depends on how much you want to tinker and how much time you have to fall down deep rabbit holes.

Mostly, these days I just use a Mac as it just does what I need it to do without much tinkering.  When I’m in the mood to tinker or if I’m doing something that requires Linux I just run it in a VM.  The two distros I mostly use are <a href="https://www.linuxmint.com/" class="hvr-wobble-skew">Mint</a> with Cinnamon DE as my daily driver and <a href="https://www.kali.org/" class="hvr-wobble-skew">Kali</a> with XFCE for security-related projects.

I guess the tl;dr is the right distro for someone is really what they are comfortable with.  IMO, the big difference between distros is the package manager.[^5] So, the answer really is go with what you know.  You don't want to be searching for things or tinkering when you need to get something done. 

## Resources

* <a href="https://wiki.archlinux.org/title/Desktop_environment" class="hvr-wobble-skew">https://wiki.archlinux.org/title/Desktop_environment</a>
* <a href="http://www.xwinman.org/" class="hvr-wobble-skew">http://www.xwinman.org/</a>

[^1]: Yes, I know that's not the actual post, but I couldn't find it again. Also, it comes up fairly often.
[^2]: Keep in mind these disks held 1.44 megabytes (MB).  I think Slackware was only 5 or 6 disks around then, while Windows 3.1 was about a dozen.
[^3]: A desktop environment (DE) bundles together a variety of components to provide common graphical user interface elements such as icons, toolbars, wallpapers, and desktop widgets. Additionally, most desktop environments include a set of integrated applications and utilities. Most importantly, desktop environments provide their own window manager, which can however usually be replaced with another compatible one. 
[^4]: A window manager (WM) is system software that controls the placement and appearance of windows within a windowing system in a graphical user interface (GUI). It can be part of a desktop environment (DE) or be used standalone.
[^5]: A package manager is the tool used to install and maintain software packages.  For example, `apt` vs `rpm` vs `yum`.