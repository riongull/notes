### Scripting tools

#### Bash scripting

###### create and print variables
``` sh
$ MYVARIABLE="Some string I want to be a variable for use in a terminal session" # ends when the terminal is closed
$ echo $MYVARIABLE # display the variable
```

###### create and execute a script
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

###### create custom commands (aliases)
``` sh
$ alias
$ alias ls='ls --color -l'
$ alias # lists curent aliases (both global and in current session)
```

###### edit .bash_profile (persisted bash configurations available every time you use Terminal)
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
