# Bash Scripting

#### About this document
This document is a reference and guide for creating and running basic bash scripts.  It assumes a knowlege of [basic terminal usage](https://github.com/riongull/notes/blob/master/terminal_notes.md).  

## Basic understanding
* scripts can run *from* any directory if...
  * a) the script is located in a directory in your `PATH` variable, __or__
  * b) you run the script with the *full* path to it's location
* add scripts to `~/bin` so they are in your `PATH`
* make scripts executable using `chmod +x <scriptname>`
* debug scripts with `bash -x`
* check which directories are in your `PATH`: `echo $PATH`
* if executable shell programs have the same name but are in different directories the program in the first directory in your path is run
* name your scripts with a .sh extension

## Create and execute a script
``` sh
$ cd ~/bin
$ nano myscript.sh # opens nano to create a new file

< # start of file contents on next line
#!/bin/bash # the 'hash-bang' tells the shell that the command interpreter should be 'bash' (execute using the program found at /bin/bash)
MYGREETING="Hello, "
if [[ $USER = Rion ]]
then echo $MYGREETING "Rion"
else echo $MYGREETING "whoever you are"
> # end of file contents, control+x to exit nano (y to save)

$ ls -l # by default the file is not exectuable
$ chmod +x myscript # gives file global executable permissions
$ ls -l # check to see permissions (should be x's in each of user/group/everyone fields now)
$ cd ~ # go back home
$ myscript # executes script, would need ./myscript if running from ~/bin
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
