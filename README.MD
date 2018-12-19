# React Boilerplate project and steps to create it

* Create project dir
* npm init (accept default)
* git init (init the repo, but pushing yet)
* create a repo on github.com
* copy the commands to push exiting repo (local) to the github
    '''
    git remote add origin https://github.com/patilkunal/egghead-react-boilerplate.git
    git push -u origin master
    '''
* npm init -y
* create src folder and index.js
* now to package, we install webpack
    npm install --save-dev webpack webpack-cli
* run 'node_modules\.bin\webpack' and see it create main.js in dist directory
* run 'node dist\main.js' to see it output Hello World
* Add following in package.json to just run 'npm run build'
    "build" : "webpack"
* we created greet.js and imported that module in index.js
* run 'npm run build -- --mode development'
