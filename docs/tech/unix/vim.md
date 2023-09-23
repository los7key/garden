---
layout: post
title: vim Cheatsheet
description: vim Cheatsheet
date: 2022-04-30
Last Updated: 2023-09-23
---

## Basic Tips and Tricks

### Navigation
* `i` - insert mode. Next keys typed are inserted into the file.
* `<Esc>` - Escape from insert mode so you can navigate and use edit commands
* `1G` - Go to line 1
* `gg` - Go to top of file
* `G` - Got to bottom of file (Shift + g)
* `S` - Places you at insert mode at the right indentation (Shift + s)
* `%` - Jump to the matching bracket/brace (Shift + 5)

### Working with files
* `:w` - Save file
* `:wq!` - Save and write file
* `:q` - Quit file with no changes
* `:q!` - Quit without saving

### Editing text  
* `=G` - Fix indentation in the whole file (Equal, Shift + G)
* `x` - Delete char at current position
* `a` - Append after current position
* `A` - Append after end of line
* `o ` - Insert new line below
* `O` - Insert new line above
* `dw` - Delete word (and copy it to clipboard)[^1]
* `dd` - Delete current line (and copy it to clipboard)[^1]
* `yy` - Yank current line (aka copy to clipboard)[^1]
* `p` - Paste clipboard
* `guu` - Lowercase line[^1]
* `gUU` - Uppercase line[^1]
* `~` - Invert case (upper->lower; lower->upper) of current character
* `ga` - Display hex, ascii value of character under cursor
* `g8` - Display hex value of utf-8 character under cursor

### Search
* set hlsearch highlight all matching patterns
* `:noh` (short for :nohlsearch) will clear the current highlighted patterns
* `/foo` - Search for the next occurance of "foo"
* `?foo` - Search for the previous occurance of "foo"

* `:%s/foo/bar/g` - Search file for all occurances of `foo` and replace with `bar` globally
* `:%s/^M//g` = Remove CRLF ^M line chars (Ctrl+V to get the ^ and then Ctrl+M to insert the M)

## Deleting empty lines
* Delete all empty lines:
```
:g/^$/d
:v/./d
```

* Delete all lines that are empty or that contain only whitespace characters (spaces, tabs):
```
:g/^\s*$/d
:v/\S/d
```
Explanation: `v` operates on lines that do not match, `\S` matches anything that is not a whitespace, and `d` deletes the flagged lines (all lines that have no characters, or that have only whitespace characters).

* Condense multiple blank lines into a single blank line.
```
:%s/\s\+$//e
:%s/\n\{3,}/\r\r/e
```
Explanation: Delete all trailing whitespace from each line, then replace three or more consecutive line endings with two line endings. `e` flag means that no error is displayed if the pattern is not found.   In the second command, `\n` in the search pattern finds newline, while `\r` in the replacement inserts a newline.
 
## Shell escapes
(More of a security tip, but seems fitting here)
    ```
    :set shell=/bin/sh
    :shell
    ```

Or alternatively:
    ```
    :!/bin/sh
    ```


## .vimrc 
```
$ cat ~/.vimrc 
set autoindent
set expandtab
set tabstop=2
set shiftwidth=2
set ignorecase
set visualbell
set mouse=a
set hlsearch
set number
syntax on
```

[^1]: Can be prefixed with number of lines that can be acted upon.  For example `dd` to delete the current line and `5dd` do delete the next 5 lines (starting with the current line). 