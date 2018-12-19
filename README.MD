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
* >npm init -y
* create src folder and index.js
* now to package, we install webpack
    npm install --save-dev webpack webpack-cli
* run 'node_modules\.bin\webpack' and see it create main.js in dist directory
* run 'node dist\main.js' to see it output Hello World
* Add following in package.json to just run 'npm run build'
    "build" : "webpack"
* we created greet.js and imported that module in index.js
* run 'npm run build -- --mode development'
* we modify greeting to getGreeting and use modern Javascript syntax
* we use Babel to modify javascript to be able to run in old browsers
    >npm i -D @babel/core @babel/cli @babel/preset-env 
* Running 'node_modules\.bin\babelsrc\greet.js' will show same output, but running 'node_modules\.bin\babelsrc\greet.js --presets=@babel/preset-env' shows output which is different
* use babel loader to pass through so that code get compiled in old version of javascript
    >npm i -D babel-loader
* add module section to webpack config to run babel loader while compiling the code.
* >npm run build to see that now we have older version of javascript generated

create a react app
* install react libraries 
    >npm i -S react react-dom prop-types
