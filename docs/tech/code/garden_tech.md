---
layout: post
title: How this garden works
description: How this garden works
date: 2022-05-12
Last Updated: 2022-06-13
---
## Introduction
I have to admit, I did cheat a bit when setting up the framework for my [garden](/).  On my journey for the technology to use for this garden, I stumbled across [The Blue Book](https://lyz-code.github.io/blue-book). It's a very simple, easy-to-use, and lightweight feeling garden.  Since it's so customizable, it has the opportunity[^1] to look better than some of the other technologies I tried. 

How did I cheat?  I only cheated in that I followed the [instructions]( https://lyz-code.github.io/blue-book/#make-your-own-digital-garden) and forked[^2] a copy of the repo.  This way I had a foundation to start with and could customize as needed and be on my way.  Who wants to reinvent the wheel?  As they say, "A good sysadmin is a lazy sysadmin".[^3] 

As usual, when I set this up a couple of months ago, I took almost 0 notes along the way.  Nothing like trying to remember all the details afterward!  This will also be another WIP as I remember what I’ve done and also as I make other changes along the way. 

## Actual useful information
Main ingredients:

* [Mkdocs](https://www.mkdocs.org/)
* [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/)
* GitHub pages 
* Custom domain

I write most of my code in [vscode]( https://code.visualstudio.com/) but I write a lot of content in a text editor (usually Word or Apple Notes) for the grammar/spelling and then copy and paste to vscode for the version control.  

All of the content is [markdown](https://en.wikipedia.org/wiki/Markdown) files.  Every commit to the GitHub repo builds the website using mkdocs and pushes it to my [garden](/).  The main config files are in `/` and the content itself lives in the docs directory.[^4]  

Monitoring is done with [uptime robot](https://uptimerobot.com/).

My garden uses the [UNLICENSE](https://unlicense.org/).

## Into the weeds
In `/` is a Makefile for mkdocs.  This builds the static site and starts up a server for testing.  By default the server that launches only runs on `localhost`, this line in the Makefile will run it on all interfaces:
```
pdm run mkdocs serve --dev-addr=0.0.0.0:80
```
Once changes have been made locally, I push my changes to the repo and viola!  The site is built.  If a build fails, I get an email saying why.  

~~I’m using [markdown link checker](https://github.com/gaurav-nelson/github-action-markdown-link-check) as a GitHub action so when new changes are pushed will verify all the links.  Currently[^5] this bit fails every run because of so many false positives, but I intend to fix that in all of my copious free time.™.  Luckily it still builds and deploys so…~~

Gave up on markdown link checker after a few days of seeing errors being defeated by the configs. I just have better things to be doing and in all honesty, mkdocs does a fine job at link checking so maybe when I get around to it I'll come up with something else to check external links.  The link checker didn't like a lot of the stuff in the [security](/tech/security/) section and I suspect most others will as well, so maybe some other time. 

As mentioned at the bottom of the [README](/), the stats are done with SCC.

DNS Records for custom domain should point to the appropriate `github.io` address



[^1]: Opportunity is key since I definitely don’t have an eye for art
[^2]: What is a fork? A GitHub fork is a copy of a repository (repo) that sits in your account rather than the account from which you forked the data from. Once you have forked a repo, you own your forked copy. This means that you can edit the contents of your forked repository without impacting the parent repo.
[^3]: https://www.thegeekstuff.com/2011/07/lazy-sysadmin/
[^4]: This can be customized in `mkdocs.yml`
[^5]: 2022-05-12


## References
https://mkdocs.readthedocs.io/en/0.12.1/
https://www.mkdocs.org/dev-guide/themes/

