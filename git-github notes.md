# Typical Git/Github Workflow Patterns

### Helpful git tutorials
* https://www.youtube.com/watch?v=E8TXME3bzNs
* https://www.youtube.com/watch?v=44E8o-xuxWo&index=1&list=PLPXsMt57rLtgpwFBqZq4QKxrD9Hhc_8L4

### Install and initialize gitclick
* https://www.youtube.com/watch?v=Q1fFY4cGfmI
* https://github.com/maximilianschmitt/gitclick
``` sh
$ npm install gitclick -g # installs gitclick utility, assumes node package manager is installed
$ gitclick # shows help file for cli commands
$ gitclick add # wizard that adds a gitclick service
# follow prompts:
# Name: e.g. github
# Hosted: Github
# Username or password: <username> e.g. riongull if github account url is https://github.com/riongull
# Password or Access Token: (follow steps video tutorial (one-time) configure github with a secure access token for gitclick)
$ gitclick list # lists your gitclick services
```
## Creating a git project (two methods)
### 1. create from local (computer terminal)
``` sh
$ cd desiredDirectory
$ mkdir "git-repo"
$ cd git-repo
$ git init # initializes a local git repo (makes a hidden ".git" folder in your present directory), assumes git is installed on computer already
$ git add . # stages file(s) in preparation to be committed.  to unstage a file, use 'git reset HEAD README.MD’
$ git commit -m "first commit, added readme document" # commits changes in preparation to be pushed to github.com.  to remove this commit and modify the file, use 'git reset --soft HEAD~1' and commit and add the file again
$ gitclick create # creates a new repository on github.com, copy the https URL for next step
$ git remote add origin https://github.com/riongull/new-git-repo.git # initiates binding between newly-created github repo and your local machine's git repo
$ git push -u origin master # finalizes the binding between local and remote git repos. command is shorthand for git push origin master —-set-upstream, I think
```

### 2. create a git project from remote (github.com)
1. sign into github.com/username
2. click repositories tab, then click "New"
3. fill out form, call the repo something like github-repo
4. nav to new repo, copy URL
5. open terminal and cd to desired directory
``` sh
$ git clone <URL> (without the arrows)
```
* this creates a folder in your current directory called github-repo on your drive
* under github-repo there's a new README.md file and a new (hidden) .git folder

## Collaborating on a git project
roles:
* *owner*: person who owns a github repo (has repo login credentials)
* *collaborator*: person who has been invited by owner to collaborate on repo
* *contributor*: person who hasn't been invited into the repo team, but whose pull requests have been accepted by owner  

### owner
#### solicit community help
* make someone a collaborator on an existing by adding them from github.com/you/your-repo,
  * gives them commit access to your repo
* and/or add guidelines to your repo instructing random people how to contribute to it

#### check the functionality of someone else's branch
``` sh
git fetch —-all # gets recent branches that may exist on github (your desktop git may not have them yet)
git branch —-list -r  # displays list of directories (including remote watching branches)
git checkout <branch_name> # checks out branch you want to operate with.  Your local files are now changed to theirs
```
* run code on local machine, test drive changes
* if there are questions or concerns, make comments on specific lines on github.com while viewing commit diff
* if all looks good, consider merging changes into master (next step below)

#### merging code into master from another branch in github repo
``` sh
$ git branch # list branches, check which on you're on (where "*" is)
$ git checkout master # get back on master branch if neccessary
$ git merge <new_branch_name> # merges (accepts) a collaborator's/contributor's work into master.  Hope there are no conflicts
$ git push origin master # pushes changes (in this case, the merged changes)
$ git branch -d new_branch_name # (optional) deletes specified branch (in this case, the merged branch) while you are on a different branch
```
* you can also delete the now-merged branch on github.com as well (snoop around there, it's there)
* tips for using branches: [paper](http:--nvie.com-posts-a-successful-git-b­ranching-model) | [summary of paper](https:--github.com-WalnutiQ-WalnutiQ-iss­ues-62)

### collaborator
#### create a new repo branch
* useful when adding a new feature (or fixing a bug)   
``` sh
$ git branch # list all branches in working folder
$ git branch <new_branch_name> # creates new branch
$ git checkout new_branch_name # switch to new branch (your local files actually change)
$ git push origin new_branch_name # adds the new branch to github.com repo
```

### contributor
#### fork project you want to contribute to
``` sh
# clone (i.e. fork) owners repo
$ git clone https://github.com/some-owner/their-repo.git # forks repo you want to work
$ git pull # syncs owner’s changes to your local drive (if some time has passed since clone
# make and commit changes to (contributors) fork of repo
$ git commit -am "message of commit" # stages all files to be committed, then commits a branch with the message.
```
* go to github.com, click "Pull Requests" > "New pull request" > "Create Pull Request"
* give pull request a description, then "Send pull request"

## Other useful tips
### stop requiring username & password in a repo
``` sh
$ git remote set-url origin git@github.com:yourUsername/yourReponame.git
```
### remove a file from github.com, but keep it locally
``` sh
$ git rm --cached localFileName
$ nano .gitignore
"localFileName" #place this text in the .gitignore file
# save and close file
# stage and commit changes
$ git commit -am "deleted private file from github, created and populated .gitignore to ignore localFileName"
$ git push
```
### reset local directory
``` sh
$ git reset --hard 31j4klt5j43klu7j635k65jkl3jr22
# replace string with SHA of commit from github.com
# makes local folders & files look like they did at a given github.com commit

```
### delete a commit from github.com
``` sh
$ git push -f origin HEAD^^^:master
# undoes 3 commits (because of three ^s from git/github) of master branch (can designate other branch)
# permanently removes a commit from git, like when you uploaded some embarrassing stuff
```
