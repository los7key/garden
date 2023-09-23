---
layout: post
title: Bash Prompts
description: Random bash tidbit
date: 2022-04-09
Last Updated: 2022-04-16
---

I have [dot files](https://github.com/jellyfishsizzle/dotfiles) that are never kept up to date, so I end up taking notes elsewhere.  

Here are some other notes I've picked up along the way.

#### Set prompt to pick up repo like zsh does

```
# Check for git branches
parse_git_branch() {
     git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
}

# Prompt (Just white for now)
# Set prompt for collapsing dirs
PROMPT_COMMAND='pwd2=$(sed "s:\([^/]\)[^/]*/:\1/:g" <<<$PWD)'
PS1='\[\e[01;37m\][\u@\h:$pwd2$(parse_git_branch)] \$ \[\e[0m\]'
export PROMPT_COMMAND="add_title;$PROMPT_COMMAND;"
```

That crazy mess above basically shortens the working directory in the prompt.  It's really nice when you’re drilled deep into a filesystem and end up in `/usr/local/share/project/files/images` and your terminal isn't very large.  It would "collapse" all the directories so the prompt will look like `/u/l/s/p/f/images`.  That is how I configure every terminal environment I use regularly.  

It makes my prompt look like `[jelly@legend:/u/l/s/p/f/images ] $`