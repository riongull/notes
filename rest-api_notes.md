# Create a RESTful API using Node, Express, & Node-restful (w/Github)

## Helpful resources
### video tutorials
* [Build a RESTful API in 5 Minutes with NodeJS - Updated](https://www.youtube.com/watch?v=p-x6WdwaJco) (uses Express)
* [In 5 minutes, REST API with Express and Node.js](https://www.youtube.com/watch?v=4XBwmMbYwsk) (uses Express)
* [Build REST APIs in Node.js with restify](https://www.youtube.com/watch?v=lXtiz_GAtBA) (uses Restify, included for reference due to popularity)

### documentation websites
* https://github.com/typicode/json-server
* http://expressjs.com/en/4x/api.html
* https://github.com/baugarten/node-restful
* http://restify.com/ (included for reference due to popularity)
* https://github.com/restify/node-restify (included for reference due to popularity)

### other resources
* http://www.meteorpedia.com/read/REST_API
* https://developers.google.com/adwords/api/docs/appendix/productsservices

## 0. Test with fake server
#### install json-server
``` sh
$ npm install -g json-server
$ cd desired-directory
$ mkdir "json-server"
$ cd "json-server"
$ nano jsonDb.json # can use atom or other text editor to create and edit file

# edit newly created file with some data, e.g.
{
  "offerings":[
    {
      "id":0,
      "name":"fruit"
    },
    {
      "id":1,
      "name":"back rubs"
    },
    {
      "id":2,
      "name":"socks"
    }
  ]
}
# save and close file

$ json-server jsonDb # or,
$ json-server --watch jsonDb.json --port 3000 # to launch on a specific port and watch for changes to file
```

## 1. Create git project
#### create git project on local drive
``` sh
$ cd desired-directory
$ mkdir "rest-api"
$ cd rest-api
$ git init # initializes a local git repo (makes a hidden ".git" folder in your present directory), assumes git is installed on computer already
$ touch "README.md" # add a readme file to repo
$ nano "README.md"
### Add a brief description, e.g. "Build RESTful api"
$ git add -A # stages file(s) in preparation to be committed.  to unstage a file, use 'git reset HEAD README.MD’
$ git commit -m "added readme file" # commits changes in preparation to be pushed to github.com.  to remove this commit and modify the file, use 'git reset --soft HEAD~1' and commit and add the file again
```
#### create and configure github repo
* Prerequisite: [install and configure gitclick](https://github.com/riongull/notes/blob/master/git-github_notes.md#install-and-initialize-gitclick)

``` sh
$ gitclick create # creates a new repository on github.com, copy the https URL for next step
$ git remote add origin https://github.com/riongull/rest-api.git # initiates binding between newly-created github repo and your local machine's git repo
$ git push -u origin master # finalizes the binding between local and remote git repos. command is shorthand for git push origin master —-set-upstream, I think
```

## 2. Create node project
#### initialize repo
``` sh
npm init
```
#### install package dependencies


## 3. Create a RESTful API server
