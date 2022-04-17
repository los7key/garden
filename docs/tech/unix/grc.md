---
layout: post
title: Add color with GRC
date: 2022-04-09
Last Updated: 2022-04-16
---
I've done a lot of work in a terminal for many years and until recently never realized how useful it would be to have some color output for commands I use frequently.  It's really helpful to see key things you are looking for in the output of a command at a glance.  Sure, the output is the same, but it makes it easier to see what you are looking for.  

There are some examples of what it looks like below.  Keep in mind I can change any of the colors, what commands use color, and what things are highlighted myself.  I'm not sure how I lived without this.

NOTE: The instructions below assume you already have python installed and that you are fairly comfortable with the command line.

Let's go over the setup and general usage so that you can give it a try and also so I can remember how it's done later down the road.  It's all in python, so it can be used pretty much anywhere.  I'm currently using it on MacOS and Linux. 

First, we'll need the actual source code.  I forked a copy for my own use so that I can keep copies of configs and share them across multiple machines.  The repo is [here](https://github.com/jellyfishsizzle/grc). 

With the source code cloned, it's just a matter of running the included install script.  NOTE: You'll need to use sudo if you go with the defaults in the install script. 

There is a section that outlines installation that has some useful information.  Basically, you run the install script and it will copy all of the bits to a reasonable place (obviously, you can change it to meet your needs).  The only trick is if you are using bash it doesn't put the config in the right place by default.  I'll tweak it in all my copious spare time.  

You're probably wondering why I wrote anything about this when there is already plenty of information on installation and usage in the readme.  Well, there is some customization I've done that I found useful to keep note of.  

I'll go over the "easy" way and then the way I did it so that all the configs are in one place and it will stay updated for other hosts.  

## The easy way
1. Change to the grc directory you cloned and run `sudo install.sh`
2. The conf.bashrc file wasn't copied to the location it is expected to be found.  Yes, I'll probably update the install script later.  For now, if you use bash, just copy grc.bashrc to /etc. 
3. For bash users add this to your `~/.bashrc`:  
`[[ -s "/etc/grc.bashrc" ]] && source /etc/grc.bashrc`  
(For zsh it would be ~/.zshrc and source /etc/grc.zsh)  
4. Source your rc file or launch a new terminal and run commands that you would expect to have colored output.

## The git way
Instead of running the install script we'll just create a bunch of sym links to point to your config files in your repo so that you can check in new and updated configs to your own repo.  For this example I'll use `~/src/rc` as the location of my project.

1. `sudo ln -s /etc/grc.bashrc ~/src/grc/grc.bashrc`
2. `sudo ln -s /etc/grc.conf ~/src/grc/grc.conf`
3. `sudo ln -s /usr/local/share/grc ~/grc/colourfiles`
4. For bash users add this to your `~/.bashrc`:  
`[[ -s "/etc/grc.bashrc" ]] && source /etc/grc.bashrc`  
(For zsh it would be ~/.zshrc and source /etc/grc.zsh)
5. Source your rc file or launch a new terminal and run commands that you would expect to have colored output.

## A few notes about customizations
The included readme contains all the information you'll need to start making customizations and adding new commands you want color for.  There were a few things not so obvious to me:

1. There needs to be a conf file for each app you want to have colored output. The config file for each app is in `/usr/local/share/grc`.  This is where colors are defined for specific output you want colored.
2. For each conf file in `/usr/local/share/grc`, there needs to be an alias for it in your grc.bashrc (or grc.zshrc). 
3. For each conf file, you have to create a corresponding entry in `/etc/grc.conf` with the name of the config file and regex to identify the command.

## Some example output

<script id="asciicast-344961" src="https://asciinema.org/a/344961.js" async data-speed=".75"></script>