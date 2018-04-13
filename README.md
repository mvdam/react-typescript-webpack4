# React Typescript Webpack v4

Experiment to setup a React project with TypeScript & Webpack v4!

Requirements
* Node.js >= v8.2


Steps
1. `npm i react react-dom --save`
2. `npm i webpack webpack-cli --save-dev`
3. `npx webpack src/index.ts`

Findings;
* For Webpack you have to install the `webpack-cli` to get it working
* Webpack 4 is not 0CJS (yet). TypeScript support is not built-in
* Unlike Parcel, Webpack does not support html as entry file
* Webpack `--mode 'development|production'` is quite nice!

4. `npm install ts-loader --save-dev`
5. Created webpack.config.js -- there goes the 0CJS...... 🤯
6. `npm install typescript --save-dev`
7. Created tsconfig.json... Webpack 0CJS is dead! 😭 ☠️
8. `npm install @types/react @types/react-dom --save-dev`

Findings;
* We now have a -working- version, but no Hot Module Reload and dev server yet...
* Checking support of CSS modules... Surprise! We need another loader!
* Also we need to setup some other configuaration to export all css to a file

9. `npm install --save-dev css-loader style-loader`
10. Added loader for CSS to webpack config
11. We also need some loaders for images, fonts etc. Lets `npm install --save-dev file-loader`



We don't want to rebuild and reload our browser all the time. So lets hook in webpack-dev-server
12. `npm install webpack-dev-server --save-dev`
13. We now need to config webpack-dev-server. Add to webpack.config.js;
    ```js
    {
        ...
        devtool: 'inline-source-map',
        devServer: {
            contentBase: './dist',
            hot: true
        },
        plugins: [
            new webpack.NamedModulesPlugin(),
            new webpack.HotModuleReplacementPlugin()
        ]
        ...
    }
    ```
    > Make sure that your `index.html` is also in this `contentBase`. Otherwise it won't refresh automatically.

14. And to start the dev server we add a script to our `package.json`
    ```json
    {
        ...
        "start": "node_modules/.bin/webpack-dev-server --open"
        ...
    }
    ```
15. When we make a change now it will refresh the browser automatically!
16. But wait! My styles aren't applied! We need to `npm install --save-dev extract-text-webpack-plugin@next`. Mind the `@next` party because it is not officially updated for Webpack v4 yet!



- npm install --save-dev mini-css-extract-plugin

Findings:
* Its a bit tricky to use such a beta release in production. This basically means that we can't use Webpack 4 yet in prods
* This is so basic functionality that it should be built-in into Webpack or has some preset for it













Bootstrapping a React Typescript project. What are the differences between Webpack 4 and Parcel Bundler?

Requirements for the new build setup
- [ ] TypeScript
- [ ] React
- [ ] CSS Modules
- [ ] Custom fonts
- [ ] Images
