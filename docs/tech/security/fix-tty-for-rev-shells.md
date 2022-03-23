# Fix TTY for rev shells

```
python3 -c "import pty;pty.spawn('/bin/bash')"

(ctrl+Z)

printf "\n\n(Rows,Cols)\n ";printf '\e[1;91m%-6s\e[m' $(stty size);printf "\n\nTerm= \e[91m$TERM\e[0m\n\n";stty raw -echo;fg;

export SHELL=bash;export TERM=xterm-256color;stty rows 20 columns 100;\echo ;echo ;read -p "Enter Rows:" ROWS;read -p "Enter Cols:" COLS;stty rows $ROWS columns $COLS && clear
```

Basically a fancy version of:

```
SHELL=/bin/bash script -q /dev/null
 Ctrl-Z
 stty raw -echo
 fg
 reset
 xterm
```
