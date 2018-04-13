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
7. Created tsconfig.json... 0CJS is dead! 😭 ☠️
8. `npm install @types/react @types/react-dom --save-dev`

Findings;
* We now have a -working- version, but no Hot Module Reload and dev server yet...
* Checking support of CSS modules... Surprise! We need another loader!
* Also we need to setup some other configuaration to export all css to a file

9. `npm install --save-dev css-loader style-loader`
10. Added loader for CSS to webpack config
11. We also need some 
12. `npm install webpack-dev-server --save-dev`
13. ...














Bootstrapping a React Typescript project. What are the differences between Webpack 4 and Parcel Bundler?