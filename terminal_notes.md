# Terminal Usage and Common Commands

#### About this guide
This document lists and explains generally-used commands on the terminal program.  Commands work on both Mac and Linux systems, but windows commands are very similar.  

### Basics

###### Opening terminal
* On a Mac, press `command`+`spacebar` to bring up Spotlight Search, then type `terminal` and hit enter.

###### Command line syntax
* Text in `this font` represents a code snippet, the name of a file, a command you execute, etc.
* Syntax
  *  In your terminal program: `YourComputers:YourPWD You$ command -with <text-in-brackets>`
    * `YourComputers:YourPWD You` shows information about your computer, user, and present working directory
    * `$` is the 'command prompt', it shows your that your terminal session is ready for your input
    * `command` is the name of the program you intend to run
    * `-with` represents options, letters or words which you include to modify the way `command` will be run
    * `<text-in-brackets>` something *you replace* (omitting `"<text-in-brackets>"`) with your own data/text
    * some other guides include `[stuff-in-brackets]`, which usually represents optional arguments or options
* Starting/Stoping
    * To exectue a command, type what's *after* the `$` in our example and hit enter/return
    * Some programs execute and finish almost immediately, others run until you stop them
    * To stop a program, press `command`+`c`
* Help
  * for help with a `command`, type `help <command-in-question>` (sometimes `info` or `man` instead of `help`)

###### navigate and display content
``` sh
$ ls # lists files (ls stands for list storage) and folders in present directory
$ ls -la # '-la' flag lists all (including hidden) files and folders with detailed view
$ cd <directory_name> # changes to specified directory, start typing (excluding "<"), then press tab to autocomplete
$ cd # changes directory to the home directory
$ cd / # go to root directory (Macintosh HD)
$ cd ~ # go to logged-in user's home directory (Rion)
$ cd - # go back to previous directory (like when you accidentally cd home and want to go back)
$ man <command_you_want_to_know_about> # displays manual for a command (e.g. man ls)
```

###### create, read/view, update/edit, and delete files and folders
``` sh
$ touch "readme.md" # creates a new file (can use without quotes for files w/o spaces)
$ nano "readme.md" # creates a new file and open editor to edit, "npm install nano" to get nano
$ mkdir "New Folder" # creates a new folder
$ cat readme.md # reads/displays file in terminal, name is from "concatenate and print", all files given as parameters are concatenated and sent to "standard output"
$ cp
$ mv "readme.md" "Read Me.md" # updates/renames file from x to y
$ mv "New Folder" "newer-folder" # updates/renames folder from x to y
$ rm "readme.md" # deletes a file (can use without quotes for files w/o spaces)
$ rm -r "New Folder" # deletes a folder (r stands for recursive)
```

###### open files
``` sh
$ open readme # opens using default program
$ open readme -a "Atom" # opens using specified program (case sensitive)
$ open . # opens the current folder in Finder
$ open . -a "Atom" # opens folder in Atom
```

###### run applications
``` sh
$ cd path_where_program_lives
$ program_name [program_command] # [] items are optional
```

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

#### Npm scripting

###### write custom script in ```package.json```
``` js
// package.json
{
  "name": "package-name",
  "version": "1.0.0",
  "description": "",
  "main": "entry-point.js",
  "dependencies": {
    "some-package": "1.0.0",
  },
  "devDependencies": {},
  "scripts": {
    "your-custom-cli-name": "echo \'any cli command can be put here\' && exit 1"
  },
  "author": "You",
  "license": "ISC"
}
```

###### run custom script
``` sh
$ npm run your-custom-cli-name
```

### other useful commands
###### top
``` sh
$ top # shows list of processes running with CPU & memory usage
# s changes update delay
# i hides all the idle processes
# k kill a given process (pid)
# f shows fields to sort by
# q quits the top program
```

###### less
```sh
$ less # description
```

###### file
```sh
$ file # description
```

###### strings
```sh
$ strings # displays the contents of a file in string format
```

###### template
```sh
$ template # describe what it does
```

### online resources
* [Detailed list of commands](https://github.com/0nn0/terminal-mac-cheatsheet)
* [Linux video series](https://www.youtube.com/watch?v=NWWvZa-qlRE&list=PLT98CRl2KxKHdOpQ-uI2QuNcQ0aEAe5bN&index=38)
* [Bash scripting video series](https://www.youtube.com/watch?v=1PoQUmy4X2M&index=19&list=PLpKIAFYBxQOWzJjInMUaKtamCshDmLjej)
