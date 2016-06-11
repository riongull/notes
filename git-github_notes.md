# Typical Git/Github Workflow Patterns

## Helpful git tutorials
### official tutorials

```sh
$ git help # basic git usage
$ git help -a # lists subcommands, follow up with 'git help <command>', e.g. 'git help branch'
$ git help -g # lists guides, follow up with 'git help <concept>', e.g. 'git help workflows'
# many help files open text documents within terminal, press "q" to escape
```
### video tutorials
* https://www.youtube.com/watch?v=E8TXME3bzNs
* https://www.youtube.com/watch?v=44E8o-xuxWo&index=1&list=PLPXsMt57rLtgpwFBqZq4QKxrD9Hhc_8L4

### reminders
* "remote" generally refers to 'on Github', "local" generally refers to 'your local computer'
* git push and git pull's arguments are, e.g.: git pull <remote-name> <local-branch-name>
* a good explanation of git push and pull and the -u (--set-upstream) flag is found [here](http://stackoverflow.com/questions/17096311/why-do-i-need-to-explicitly-push-a-new-branch/17096880#17096880)

## Creating a git project (three methods)

#### 1. create from scratch starting from github.com ([details](https://help.github.com/articles/creating-a-new-repository/))

1. sign into github.com/username  
2. click repositories tab, then click "New"  
3. fill out form, call the repo something like github-repo  
4. nav to new repo, copy URL  
5. open terminal and cd to desired directory  
6. `git clone <URL>`
  * this creates a folder in your current directory called github-repo on your drive
  * under github-repo there's a new README.md file and a new (hidden) .git folder

#### 2. create from scratch starting from local computer terminal
1. install gitclick [(see below)](https://github.com/riongull/notes/blob/master/git-github_notes.md#install-and-initialize-gitclick)
2. run following commands:

```sh
$ cd desired-directory
$ mkdir "new-git-repo"
$ cd new-git-repo
$ git init # initializes a local git repo (makes a hidden ".git" folder in your present directory), assumes git is installed on computer already
$ nano README.md # (optional) creates a markdown file called README.  Give it a basic description of the repo.  Save and close.
$ git add . # (optional) stages new file(s) in preparation to be committed.  to unstage a file, use 'git reset HEAD README.MD’
$ git commit -m "first commit, added README document" # (optional) commits changes in preparation to be pushed to github.com.  to remove this commit and modify the file, use 'git reset --soft HEAD~1' and commit and add the file again
$ gitclick create # creates a new repository on github.com, copy the https URL for next step
$ git remote add origin https://github.com/riongull/new-git-repo.git # initiates binding between newly-created github repo and your local machine's git repo
$ git push origin master --set-upstream # finalizes the binding between local and remote git repos (--set-upstream = -u).
```

#### 3. create a new private repo based on and existing repo ([reference](http://stackoverflow.com/a/30352360/6451948))

&nbsp;&nbsp;1\. create a new (private) repo from scratch using either method above.  
&nbsp;&nbsp;2\. mirror duplicated the public repo, as follows:
```sh
$ git clone --bare https://github.com/exampleuser/public-repo.git
$ cd public-repo.git # some comment
$ git push --mirror https://github.com/yourname/private-repo.git
$ cd ..
$ rm -rf public-repo.git
```

&nbsp;&nbsp;3\. clone the private repo so you can work on it:
```sh
$ git clone https://github.com/yourname/private-repo.git
$ cd private-repo
# make some changes
$ git commit
$ git push origin master
```

&nbsp;&nbsp;4\. (optional) to pull new hotness from the public repo:
```sh
$ cd private-repo
$ git remote add public https://github.com/exampleuser/public-repo.git
$ git pull public master # Creates a merge commit
$ git push origin master
```

## Collaborating on a git project
roles:
* _owner_: person who owns a github repo (has repo login credentials)
* _collaborator_: person who has been invited by owner to collaborate on repo
* _contributor_: person who hasn't been invited into the repo team, but whose pull requests have been accepted by owner  

### owner
#### solicit community help
* make someone a collaborator on an existing by adding them from github.com/you/your-repo,
  * gives them commit access to your repo
* add guidelines to your repo instructing people how to contribute to it

#### check the functionality of someone else's branch

```sh
$ git branch —-list -a  # lists all directories (including remote watching branches); use -r for just remote branches
$ git checkout <branch_name> # checks out branch you want to operate with.  Your local files are now changed to branch_name's files (can checkout remote repos)
$ git log -1 # shows the last commit on the current branch
$ git fetch —-all # downloads objects (files) and refs (branches and/or tags) from another repo (like github.com; your desktop git repo may not have them yet)
$ git branch --set-upstream-to=origin/<remote_branch> <current_branch> # (optional/if neccessary) sets up tracking (syncing ability) between a remote (e.g. github) repo and a local (on hard drive) repo
$ git merge # merge remote branch with local branch (make sure to get back on local branch before executing this)
$ git pull # basically git fetch + git merge. If 'git branch --set-upstream-to' is completed this will sync local_branch with remote_branch's changes
```
* run code on your local machine, test drive changes
* if there are questions or concerns, make comments on specific lines on github.com while viewing commit diff
* if all looks good, consider merging changes into master (next step below)
* [note regarding the diffeence between git fetch and git pull](http://stackoverflow.com/questions/14894768/git-fetch-vs-pull-merge-vs-rebase)

#### merging code into master from another branch in github repo
```sh
$ git branch # list local branches, check which on you're on (where "*" is)
$ git checkout master # get back on master branch if necessary
$ git merge <branch_name> # merges (accepts) a collaborator's/contributor's work into master, from <branch_name>
$ git push origin master # pushes changes (in this case, the merged changes) from local to remote
$ git branch -d <branch_name> # (optional) deletes specified branch (in this case, the merged branch) while you are on a different branch
```
* you can also delete the now-merged branch on github.com as well (snoop around there, it's there)
* tips for using branches: [paper](http://nvie.com/posts/a-successful-git-branching-model/) | [summary of paper](https://github.com/WalnutiQ/walnut/issues/62)

### collaborator
#### create a new repo branch
* useful when adding a new feature (or fixing a bug)

```sh
$ git branch # list all branches in working folder
$ git branch <branch_name> # creates new branch
$ git checkout branch_name # switch to new branch (your local files actually change)
$ git push origin branch_name # adds the new branch to github.com repo
```

### contributor
#### fork project you want to contribute to
```sh
# clone (i.e. fork) owners repo
$ git clone https://github.com/some-owner/their-repo.git # forks repo you want to work
$ git pull # syncs owner’s changes to your local drive (if some time has passed since clone)
# make and commit changes to (contributors) fork of repo
$ git commit -am "message of commit" # stages all files to be committed, then commits a branch with the message.
```
* go to github.com, click "Pull Requests" > "New pull request" > "Create Pull Request"
* give pull request a description, then "Send pull request"

## Other useful tips
#### Install and initialize gitclick
* https://www.youtube.com/watch?v=Q1fFY4cGfmI
* https://github.com/maximilianschmitt/gitclick

```sh
$ npm install gitclick -g # installs gitclick utility, assumes node package manager is installed
$ gitclick # shows help file for cli commands
$ gitclick add # wizard that adds a gitclick service
# follow prompts:
# Name: e.g. github
# Hosted: Github
# Username or password: <username> e.g. riongull if github account url is https://github.com/riongull
# Password or Access Token: (follow steps in video tutorial (one-time) to configure github with a secure access token for gitclick)
$ gitclick list # lists your gitclick services
```

#### stop requiring username & password in a repo
```sh
$ git remote set-url origin git@github.com:yourUsername/yourReponame.git
```
#### remove a file from github.com, but keep it locally
```sh
$ git rm --cached localFileName
$ nano .gitignore
"localFileName" #place this text in the .gitignore file
# save and close file
# stage and commit changes
$ git commit -am "deleted private file from github, created and populated .gitignore to ignore localFileName"
$ git push
```
#### reset local directory
```sh
$ git reset --hard 31j4klt5j43klu7j635k65jkl3jr22
# replace string with SHA of commit from github.com
# makes local folders & files look like they did at a given github.com commit

```
#### delete a commit from git/github.com
```sh
$ git push -f origin HEAD^^^:master
# undoes 3 commits (because of three ^s from git/github) of master branch (can designate other branch)
# permanently removes a commit from git, like when you uploaded some embarrassing stuff
```
#### display a log of commits
```sh
$ git log -3
# shows the last 3 commits on the current branch
```
