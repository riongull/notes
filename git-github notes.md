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
```
Follow prompts:
* name: e.g. github
* hosted: Github
* username or password: <username> e.g. riongull if github account url is https://github.com/riongull
* Password or Access Token: (follow steps video tutorial (one-time) configure github with a secure access token for gitclick)
``` sh
$ gitclick list # lists your gitclick services
```
## Create a git project (two methods shown)
### * create from local (computer terminal)
``` sh
$ cd desiredDirectory
$ mkdir "git-repo"
$ cd git-repo
$ git init # initializes a local git repo (makes a hidden ".git" folder in your present directory), assumes git is installed on computer already
$ git add . # stages file(s) in preparation to be committed.  To unstage a file, use 'git reset HEAD README.MD’
$ git commit -m "first commit, added readme document" # commits changes in preparation to be pushed to github.com.  To remove this commit and modify the file, use 'git reset --soft HEAD~1' and commit and add the file again.
$ gitclick create # copy ssh URL
$ git remote add origin https://github.com/riongull/new-git-repo.git
$ git push -u origin master # shorthand for git push origin master —-set-upstream, I think
```

### * create a git project, from remote (github.com)
1. Sign into github.com/username
2. Click repositories tab, then click "New"
3. Fill out form, call the repo something like github-repo
4. Nav to new repo, copy URL
5. Open terminal and cd to desired directory
``` sh
$ git clone <URL> (without the arrows)
```
* This creates a folder in your current directory called github-repo on your drive
* Under github-repo there's a new README.md file and a new (hidden) .git folder

##
### create a new branch of a repo
``` sh
$ git branch <branch_name> # creates new branch
$ git branch # not sure what this does at this point, REVISE
$ git commit -am "message of commit" # stages all files to be committed, then commits a branch with the message.
```

### Merging code into master from another branch in github repo
1. git fetch —-all to get recent branches that may exist on github.
2. git branch —-list -r  to see the list of directories (including remote watching branches)
3. git checkout <branch_name> # checks out branch you want to develop in
4. git merge <branch_name> #

### Stop requiring username & password in a repo
``` sh
$ git remote set-url origin git@github.com:yourUsername/yourReponame.git
```
### Working together from perspective of person that doesn’t own the main repo
``` sh
$ git clone https://github.com/yourUsername/yourReponame.git # forks repo you want to work
$ git pull # if you’ve already done git clone and you want to sync owner’s changes to your local drive
```
1. make and commit changes to (contributors) fork of repo
2. go to github.com, click "Pull Requests" > "New pull request" > "Create Pull Request"
3. give pull request a description, link through "Send pull request"

### Working together from perspective of person that owns the main repo
1. some stuff
2. some more stuff

### Remove file from github.com repo but keep it locally
``` sh
git rm —cachhed localFileName
```
