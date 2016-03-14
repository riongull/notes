# Git-tracked Meteor Project Workflow

### 1. Create a new git repo
``` sh
$ cd desiredDirectory
$ mkdir "new-git-repo"
$ cd new-git-repo
$ git init # initializes a local git repo
$ gitclick create # see
$ git remote add origin https://github.com/riongull/new-git-repo.git
$ git push -u origin master # shorthand for git push origin master —-set-upstream, I think
```

### 2. Create a meteor project in git project
```sh
$ meteor create <meteor-project-name> (without the arrows)
```
* This adds a folder called meteor-project-name under github-repo-name
* It also adds meteor-project-name.html/.css/.js files and a .meteor folder under meteor-project-name

### starting from previous step
``` sh
$ cd ./github-repo-name # nav in terminal to git folder
$ git status # checks status of git
```
###### The meteor-project-name should be listed as tracked, but not added (it’s red)
``` sh
$ git add meteor-project-name # adds folder to git staging (ready to commit)
```
###### use git add -A (or git add . ?) to add (stage) all files in the directory
``` sh
$ git status # files and folders should be green now
$ git commit -m "description of new changes" # commits changes to git (not github yet)
$ git push # pushes (uploads) newly committed files to github (finally syncing local and remote repos)
```
###### If working in a team
``` sh
 git pull # pulls in changes from the remote master repo before pushing any changes up
```
