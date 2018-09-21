https://medium.com/codestar-blog
https://medium.com/@mvdam

# Parcel Bundler vs. Webpack 4 ⚔️️
> Setting up a fresh TypeScript React project

Starting up a new frontend project can be quite intensive. Most time will vanish in setting up the build process. We all know the pains of setting up Webpack with loaders and configuration files.

But things might have changed. We have two (relatively) new kids on the block;

* [Parcel Bundler](https://github.com/parcel-bundler/parcel), released December 2017
* [Webpack 4](https://github.com/webpack/webpack), released on February 2018

## #0CJS
There is quite some fuzz around 0CJS (Zero Configuration JavaScript) lately. It's all about great developer experience. This makes perfect sense for setting up build tools like Parcel or Webpack. For more advanced projects it may take huge effort to set it up correctly.

Parcel claims to be a blazing fast, zero configuration web application bundler. That all sounds nice, but does it really work out of the box? And how does Webpack 4 compare to Parcel?

## App requirements
Before going any further, let's determine some requirements for our application. For a professional web application we might want to have support for the following technology.
- React
- TypeScript (TSX)
- Being able to import:
    - JavaScript modules (obviously)
    - CSS Modules
    - Fonts
    - Images
- Development server capabilities

<div align="center">
    <br>
    <br>
    <a href="https://github.com/webpack/webpack">
    <img width="200" height="200" src="https://webpack.js.org/assets/icon-square-big.svg">
    </a>
    <br>
    <br>
</div>

## Setup the build using Webpack 4
The focus of the Webpack team for version 4 was mainly on performance and improved default configuration. For example, Webpack runs in production mode by default. And for some JS-only projects it even works out-of-the-box without any configuration.

Since we want to build a slightly more advanced application, we still need to configure a lot of things to get it to work. This is a bit disappointing, because every project needs some CSS and images to look nice. It should be great if these basic requirements would work out-of-the-box.

*Configuring loaders:*
```js
rules: [
    {
        test: /\.tsx?$/,
        use: 'ts-loader',
        exclude: /node_modules/
    },
    {
        test: /\.css$/,
        use: [
            {
                loader: "style-loader"
            },
            {
                loader: "css-loader",
                options: {
                    modules: true,
                    importLoaders: 1,
                    localIdentName: "[name]_[local]_[hash:base64]",
                    sourceMap: true,
                    minimize: true
                }
            }
        ]
    }
]
```

For our requirements we need to set up the file loaders for TypeScript, CSS modules, Fonts and images in a `webpack.config.js` file. Unfortunately, we still need the `ExtractTextPlugin` to be able to bundle all the CSS of the application to a single file.

*Configuring plugins:*
```js
plugins: [
    new webpack.NamedModulesPlugin(),
    new webpack.HotModuleReplacementPlugin(),
    new webpack.ExtractTextPlugin()
]
```

The last step in setting up the build is configuring the development server with Hot Module Reloading. This is also not included in the default Webpack configuration and requires some extra dependencies.

*Configuring devserver:*
```js
devServer: {
    contentBase: './dist',
    hot: true
}
```

Even with the improved defaults of Webpack 4, setting up a new project is still quite a struggle. All the loaders and plugins are still needed and only a JavaScript loader is enabled by default. But this has also some benefits. You are very flexible in how you want to configure Webpack. And that is definitely the strength of Webpack.

### What's awesome about Webpack 4?
* Almost everything is configurable
* Large community
* Greatly improved compilation speed compared to v3 ([source](https://medium.com/webpack/webpack-4-released-today-6cdb994702d4))
* Well-funded & proven contributors
* Improved default configuration

### What's nahsome about Webpack 4?
* Almost everything is configurable (and needs to be configured)
* Initial setup is still quite intensive
* Basic stuff like CSS modules doesn't work out of the box
* Not all documentation and plugins are ready for v4

<div align="center">
    <br>
    <br>
    <img alt="Parcel" src="https://user-images.githubusercontent.com/19409/31321658-f6aed0f2-ac3d-11e7-8100-1587e676e0ec.png" width="749">
    <br>
    <br>
</div>

## Setup the build using Parcel Bundler
Probably one of the most popular new build tools is Parcel Bundler. Is it really as fast and easy to configure as they promise? Let's find out by setting up our new project.

One great feature of Parcel is that it supports an `index.html` as entry point. Using this HTML file, it automatically will bundle all references in that file. So, when we create an `index.js` file and include it in the `index.html`, Parcel will also look in the `index.js` file and bundle all the required modules.

This will even work for TypeScript files! So we can easily include an `index.ts` file in the `index.html` and Parcel will automatically compile TypeScript to JavaScript. TSX files are also supported.

*index.html:*
```html
<html>
<head>
    <title>React Parcel TypeScript Example</title>
</head>
<body>
    <div id="root"></div>
    <script src="index.ts"></script>
</body>
</html>
```

For getting CSS modules to work with Parcel we need a little bit of configuration. Simply adding a `.postcss` file `{"modules": true}` in the root dir will do the trick.

*index.ts:*
```ts
import * as React from 'react'
import * as ReactDOM from 'react-dom'

import { App } from './containers/App'

ReactDOM.render(
  <App/>,
  document.getElementById('root')
)
```

*App.tsx:*
```tsx
import * as React from 'react'
import * as styles from './App.css'

export const App = (props) =>
    <div className={styles.app}>
        {props.children}
    </div>
```

This all sounds great right? Almost no configuration and very powerful by default. Until you want to customize your build for more advanced usages. For example, being able to import Markdown files. Therefore, you have to install (or write your own) plugins.

Every NPM dependency which name starts with `parcel-plugin-...` is recognized as Parcel plugin and enabled automatically. This makes it easy to extend but it is less transparent than a single configuration file.

### What's awesome about Parcel Bundler?
* Very quick to setup
* For most projects this is a plug-n-play solution
* Development server is built-in
* Very fast compile times ([source](https://github.com/parcel-bundler/parcel#benchmarks))
* `index.html` as entry point

### What's nahsome about Parcel Bundler?
* Custom configuration requires (writing) a Parcel plugin
* Lots of magic is going on in the background
* Relatively small community (still)
* Have to prove itself future proof

## And the winner is...?
You might have noticed that setting up a new project using Webpack 4 is more about writing configuration than actually writing your application code. Setting this up with Parcel actually begins with writing the application itself. Which makes you feel great as a developer because of the instant results you got!

But which one is the winner? The new kid, Parcel, or the mature and experienced Webpack? Well, it's not that simple.

Parcel is great to set up new projects fast. This can be very helpful for R&D or pet-projects. It might be a good fit to replace Webpack with Parcel, but it has to prove that it can evolve to be as mature as Webpack is today.

Webpack is the safe choice. It has been around for quite some years, has a large community and is very mature. The flexibility makes it perfect for large projects that needs advanced configuration.
The developer experience may not be as good as with Parcel, but the team is already working on Webpack 5 which looks very promising. Features as `Presets` and `CSS/HTML/File Module Types` should drastically improve the process of setting up a new application.
