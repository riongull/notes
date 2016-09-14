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
