# Bash Scripting

#### About this guide
This document is a reference and guide for creating and running basic bash scripts   

## Basic understanding
* 

## Create and print variables
``` sh
$ MYVARIABLE="Some string I want to be a variable for use in a terminal session" # ends when the terminal is closed
$ echo $MYVARIABLE # display the variable
```

## Create and execute a script
``` sh
$ nano myscript
# write file with the following text in nano

#!/bin/bash # (tells the shell that the command interpreter should be bash)
ls
MYVARIABLE="I executed my script"
echo $MYVARIABLE # display the variable
# save and exit out of nano

$ chmod +x myscript # gives file executable permissions
$ ls -l # check to see permissions (should be x's in each of user/group/everyone fields)
$ ./myscript # executes script
```

## Create custom commands (aliases)
``` sh
$ alias
$ alias ls='ls --color -l'
$ alias # lists curent aliases (both global and in current session)
```

## Edit `.bash_profile`
Your `.bash_profile` file controls how your bash terminal session looks and operates.  Changes made to this file will persist configuration changes to all subsequent terminal sessions.

``` sh
$ cd ~/
$ nano .bash_profile

# edit the file with custom aliases, custom variables, and/or custom scrips, for example
echo "custom aliases:"
echo "'code' -> 'cd ~/code'"
echo "'ls' -> 'ls -la'"
alias code="cd ~/code"
alias ls="ls -la"
MYVARIABLE="Here is some text that will show in the terminal window upon open"
echo $MYVARIABLE # display the variable
# save and close file

$ [ctrl+t] # opens a new tab
```
see [here](http://www.joshstaiger.org/archives/2005/07/bash_profile_vs.html) to compare .bashrc vs. .bash_profile files
