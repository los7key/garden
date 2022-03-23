# Bash prompts

I have dot files, but sometimes it's just not enough.  Here are some other notes I've picked up along the way.

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

