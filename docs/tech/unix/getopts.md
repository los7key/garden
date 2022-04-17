---
layout: post
title: Bash getopts
description: Getopts reminder
date: 2022-04-16
---
Not to be confused with `getopt`, `getopts` is for dealing with command line variables that are more complex than just needing to grab the first or second variable.

I like to reuse code when I can or at least leave myself enough information to use it again.  It had been a long time since I used
`getopts` and I liked how flexible it is to use when dealing with a lot of command-line variables.  I wrote the code for a work project and since the repo isn't public, I just wanted to capture a few key pieces.  Obviously, the main one is that `getopts` doesn't deal with long options very well, but apparently `getopt` does, but is more complicated and less flexible.  So here we are.

## Example

We start with a while loop to check each option as it is read. A `:` after the letter indicates that there is a required value that goes with that flag.  Letters/options can be touching but a `:` at the beginning means to silence the warnings that are generated so you can use your own error checking.  The options are pulled in and then you just step through them with a case statement.

```
while getopts "m:b:r:l:" OPTS; do 

  case $OPTS in
     m)
       if [ $OPTARG = "start" ]; then
         STATUS="start"
       elif [ $OPTARG = "stop" ]; then
	 STATUS="stop"
       elif [ $OPTARG = "reload" ]; then
	 STATUS="reload"
       elif [ $OPTARG = "status" ]; then
         STATUS="status"
       else
	 echo "No option picked"
       fi
       ;;
     b)
       if [ $STATUS != "start" ]; then
         echo "'start' required for this option"
         exit 2
       else
         STATUS="start"
         BSTATUS="1"
         BRANCH="$OPTARG" 
         echo "Custom branch is: $BRANCH"
       fi 
       ;;
     r)
       if [ $STATUS != "start" ]; then
         echo "'start' required for this option"
         exit 2
       else
         STATUS="start"
         CSTATUS="1"
         CRULES="$OPTARG"
         echo "Custom rules file: $CRULES"
       fi 
       ;;
     l)
       if [ $STATUS != "start" ]; then
         echo "'start' required for this option"
         exit 2
       else
         STATUS="start"
         BLOCK="$OPTARG"
	 if [ $BLOCK = off ]; then
	   echo "Pass mode enabled"
	 else
	   BLOCK="on"
	 fi
       fi 
       ;;
     *)
      cmd_usage
      break
      ;;

  esac
done
```

## References
https://www.computerhope.com/unix/bash/getopts.htm