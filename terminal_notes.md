# Typical Terminal Commands

### navigate and display content
``` sh
ls # lists files (ls stands for list storage) and folders in present directory
ls -la # '-la' flag lists all (including hidden) files and folders with detailed view
cd <dir name> # changes to specified directory, start typing (excluding "<"), then press tab to autocomplete
cd # changes directory to the home directory
cd / # go to root directory (Macintosh HD)
cd ~ # go to logged-in user's home directory (Rion)
cd - # go back to previous directory (like when you accidentally cd home and want to go back)
man <command_you_want_to_know_about> # displays manual for a command (e.g. man ls)
```

### create, read/view, update/edit, and delete files and folders
``` sh
$ touch "readme.md" # creates a new file (can use without quotes for files w/o spaces)
$ nano "readme.md" # creates a new file and open editor to edit, "npm install nano" to get nano
$ mkdir "New Folder" # creates a new folder
$ cat readme.md # reads/displays file in terminal
$ mv "readme.md" "Read Me.md" # updates/renames file from x to y
$ mv "New Folder" "newer-folder" # updates/renames folder from x to y
$ rm "readme.md" # deletes a file (can use without quotes for files w/o spaces)
$ rm -r "New Folder" # deletes a folder (r stands for recursive)
```

### open files
``` sh
open readme # opens using default program
open readme -a "Atom" # opens using specified program (case sensitive)
open . # opens the current folder in Finder
open . -a "Atom" # opens folder in Atom

```

### run applications
``` sh
$ cd path_where_program_lives
$ program_name [program_command] # [] items are optional
```

### other random commands
##### top
``` sh
$ top # shows list of processes running with CPU & memory usage
# s changes update delay
# i hides all the idle processes
# k kill a given process (pid)
# f shows fields to sort by
# q quits the top program
```
##### create and print variables
``` sh
$ MYVARIABLE="Some string I want to be a variable for use in a terminal session" # ends when the terminal is closed
$ echo $MYVARIABLE # display the variable
```

##### create and execute a script
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

##### create custom commands (aliases)
``` sh
$ alias
$ alias ls='ls --color -l'
$ alias # lists curent aliases (both global and in current session)
```

##### edit .bash_profile (persisted bash configurations available every time you use Terminal)
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

### online resources
* more detailed list of commands found [here](https://github.com/0nn0/terminal-mac-cheatsheet/wiki/Terminal-Cheatsheet-for-Mac-(-basics-))
* nice [video](https://www.youtube.com/watch?v=1PoQUmy4X2M&index=19&list=PLpKIAFYBxQOWzJjInMUaKtamCshDmLjej) series on linux commands
* bash scripting [video series](https://www.youtube.com/watch?v=NWWvZa-qlRE&list=PLT98CRl2KxKHdOpQ-uI2QuNcQ0aEAe5bN&index=38)
