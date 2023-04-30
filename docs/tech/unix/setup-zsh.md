---
layout: post
title: Setting up zsh
description: Setting up zsh
date: 2022-04-21
Last Updated:
---
I've been a long time BASH person because I've been using some flavor of UNIX for so long that some of the functions are now muscle memory.  However, I've decided to give zsh a shot (again)[^1] and this time I'm really liking it.  I like that it has a lot of the BASH things I like plus all the fancy zsh things like plugins.  With some plugins you even get FISH shell features. 

## Prerequisites

1. Xcode cmd line tools
2. oh-my-zsh

### Install ohmyzsh

```
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

### Add to .zshrc
plugins=(git
        [sudo](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/sudo)
        [zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)[^2]
        [zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting/blob/master/INSTALL.md)
        )

To fix[^3] zsh colors add this to .zshrc:
```
export CLICOLOR=1
export LSCOLORS=ExGxBxDxCxEgEdxbxgxcxd
```

Some themes I like:

- afowler
- bira <— My current theme (20220421)
- gentoo
- mortalscumbag

## Append bash_history to zsh_history
```
cat ~/.bash_history | uniq | sed "s/^/\: $(date +%s)\:0;/" >> ~/.zsh_history
```

## Resources
https://gabrieltanner.org/blog/customizing-terminal-using-ohmyzsh


[^1]: I don't remember why I stopped using it.  It had some great features but it wasn't compatible with something...
[^2]: Don't forget to `source ./zsh-syntax-highlighting/zsh-syntax-highlighting.zsh` in `~/.zshrc`
[^3]: Why wouldn't you have blue directories?  BAD ZSH!