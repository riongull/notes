# Terminal Usage and Common Commands

#### About this guide
This document lists and explains generally-used commands on the terminal program.  Commands work on both Mac and Linux systems, but windows commands are very similar.  

### Basics

###### Opening terminal
* On a Mac, press `command`+`spacebar` to bring up Spotlight Search, then type `terminal` and hit enter.

###### Command line syntax
* Text in `this font` represents a code snippet, the name of a file, a command you execute, etc.
* Syntax
  * Example prompt & command: `Computer:Directory You$ command -with <text-in-brackets>`
    * `YourComputers:YourPWD You` shows information about your computer, user, and present working directory
    * `$` is the 'command prompt', it shows your that your terminal session is ready for your input
    * `command` is the name of the program you intend to run
    * `-with` represents options (letters or words) which you include to modify the way `command` will be run
    * `<text-in-brackets>` is something *you replace* (omitting `"<text-in-brackets>"`) with your own data/text
    * some guides include `"text-in-quotes"`, which typically has the same intention as `<text-in-brackets>`
    * some guides include `[text-in-brackets]`, which usually represents optional arguments (nameed options)
    * some guides include `(text-in-parentheses)`, which can be replaced with `true` or `false` as an option  

* Starting/Stoping
    * To exectue a command, type what's *after* the `$`, `command -with <text-in-brackets>` in our example, and hit enter
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

###### create/write, read/view, update/edit, and delete/remove files and folders
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

###### Use variables
``` sh
$ MYVARIABLE="Some string I want to be a variable for use in a terminal session" # ends when the terminal is closed
$ echo $MYVARIABLE # display the variable
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
* [Intro to bash scripting video series](https://www.youtube.com/watch?v=NWWvZa-qlRE&list=PLT98CRl2KxKHdOpQ-uI2QuNcQ0aEAe5bN&index=38)
* [Intro to advanced bash usage](https://www.youtube.com/watch?v=uqHjc7hlqd0)
