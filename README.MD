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

## Create a react app
* install react libraries 
    >npm i -S react react-dom prop-types
* Create App.js to render Hello World in H1 tag
* Modify index.js to use Reach and App module to render the page
* Babel needs react preset tot be able underdtand JSX tags
    >npm i -D @babel/preset-react
* Update the 'presets' in webpack config and add the new preset from above
* Run 'npm run build' to see our app compiles fine
* We need index.html file as entry point to our Web app. We can let webpack generate it for us
>npm i -D html-webpack-plugin
* update webpack config to use it. Add plugins property. And then run 'npm run build' to see generated index.html in dist folder
* loading index.html is blank since it does not have div tag for React to write the DOM elements to.
* lets create boiler plate html for that purpose
* create index.html in src folder with the div tag of id app. And modify HtmlWebpackPlugin in webpack config to now take the template as src/index.html to generate the final index.html
* Now the building is manual. We can run webpack in watch mode to auto build on a change
* We have two different runs in package.json. We can create two different webpack config based on the mode of operation (like dev and prod)
* install webpack-merge 
> npm i -D webpack-merge
* Rename webpack.config.js to webpack.config.base.js and create two new files webpack.config.dev.js and webpack.config.prod.js
* Use the merge plugin to now extend the base config to individual config type by passing object with properties to override.
* verify by 'npm run build' and 'npm run dev' to see app.bundle.js contents
* To run a webserver to serve the files install webpack-dev-server as Dev dependency using npm
>npm i -D webpack-dev-server
* Update the package.json to now run webpack-dev-server instead of webpack --watch.
* Browse to localhost:8080 to see the app and any change will recompile and force browser to reload the page.
* To update the port update dev webpack and add devServer section.

