# React Boilerplate project and steps to create it

* Create project dir
* npm init (accept default)
* git init (init the repo, but pushing yet)
* create a repo on github.com
* copy the commands to push exiting repo (local) to the github
    > git remote add origin https://github.com/patilkunal/egghead-react-boilerplate.git
    > git push -u origin master


* Re-Initialize the project 
    > npm init -y
* create src folder and index.js
* now to package, we install webpack
    > npm install --save-dev webpack webpack-cli
* run 'node_modules\.bin\webpack' and see it create main.js in dist directory
* run 'node dist\main.js' to see it output Hello World
* Add following in package.json so that we can run 'npm run build'
    "build" : "webpack"
* we created greet.js and imported that module in index.js
* Run 
    > npm run build -- --mode development
* we modify greeting to getGreeting and use modern Javascript syntax
* we use Babel to modify javascript to be able to run in old browsers
    > npm i -D @babel/core @babel/cli @babel/preset-env 
* Running 'node_modules\.bin\babelsrc\greet.js' will show same output, but running 'node_modules\.bin\babelsrc\greet.js --presets=@babel/preset-env' shows output which is different
* use babel loader to pass through so that code get compiled in old version of javascript
    > npm i -D babel-loader
* add module section to webpack config to run babel loader while compiling the code.
* 'npm run build' to see that now we have older version of javascript generated

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
* When debugging the app you see the compiled code rather than the original source code. Use source-map to see the original source. Add property devtool to webpack config file. You want this only in development mode.

## Extending the App
*  Support for the experimental syntax 'classProperties' isn't currently enabled. We need to install babel proposal plugin
    > npm i -D @babel/plugin-proposal-class-properties
* Update base webpack config to add this as plugins section and run 'npm run dev' to see the compilation works fine.

## Add CSS to the app 
* To add CSS to the app, we need babel plugin parse the CSS files.
    >npm i -D css-loader style-loader
* And update the webpack base to use this css loader
* create styles.css and import it in index.js

## Analyze webpack bundles
    >npm i -D webpack-bundle-analyzer
* Add to prod webpack config

```javascript
const merge = require('webpack-merge')
const {BundleAnalyzerPlugin} = require('webpack-bundle-analyzer')
const baseConfig = require('./webpack.config.base')

module.exports = merge(baseConfig, {
  mode: 'production',
  plugins: [new BundleAnalyzerPlugin()]
``` 

* By default it serves over http, but it can also be configured to create static report.html and the filename of report file can also be configured

```JSON
  plugins: [new BundleAnalyzerPlugin({
      analyzerMode: 'static',
      openAnalyzer: false,
      reportFilename: 'bundle_sizes.html'
  })]
```

## Externalize JS files to pull from CDN 
* Vendor JS files can be pulled from external CDN by configuration in webpack config. This is only recommended for production config

```json
module.exports = merge(baseConfig, {
  mode: 'production',
  plugins: [new BundleAnalyzerPlugin({
    analyzerMode: 'static',
    openAnalyzer: false,
    reportFilename: 'bundle_sizes.html'
  })],
  externals: {
    react: 'React',
    'react-dom': 'ReactDOM'
  }
})
````

Update index.html to load the react libraries from CDN

```html
<body>
  <div id="app"></div>
  <% if(process.env.NODE_ENV === 'production') { %>
  <script crossorigin src="https://unpkg.com/react@16/umd/react.production.min.js"></script>
  <script crossorigin src="https://unpkg.com/react-dom@16/umd/react-dom.production.min.js"></script>
  <% } %>
</body>
```
