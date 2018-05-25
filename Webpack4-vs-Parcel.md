https://medium.com/codestar-blog
https://medium.com/@mvdam

## Parcel Bundler versus Webpack 4
> Setting up a fresh TypeScript React project

Starting up a new frontend project can be quite intensive. Most time will vanish in setting up the build process. We all know the pains of setting up Webpack with loaders and configuration files.

But things might have changed. We have two -new- kids on the block;

* [Parcel Bundler](https://github.com/parcel-bundler/parcel), released December 2017
* [Webpack 4](https://github.com/webpack/webpack), released on February 2018

### #0CJS
There is quite some fuzz around 0CJS (Zero Configuration JavaScript) lately. Its all about great developer experience. This makes perfect sense for setting up build tools like Parcel or Webpack. For more advanced projects it may take huge effort to set it up correctly.

Parcel claims to be a Blazing fast, zero configuration web application bundler. That all sounds nice, but does it really work out of the box? And how does Webpack 4 compares to Parcel?

### App requirements
Before going any further, lets determine some requirements for our application. For a professional web application we should at least have support for the following technology.
- React
- TypeScript (TSX)
- Being able to import:
    - JavaScript modules (obviously)
    - (S)CSS Modules
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

#### Setup the build using Webpack 4
blabla

* Create `webpack.config.js` file
* Configure loaders for TypeScript, CSS modules, Fonts and images
* Configure dist folder
* Create an entry point `index.js`
* For production build support we also need to configure source maps and `ExtractTextPlugin` to be able to bundle all the CSS
* Configure dev server with HMR
* Run `webpack`
* Optional: create a `tsconfig.json` file for the TypeScript configuration

**Pros**
* Almost anything is configurable
* Large community
* Greatly improved compilation speed compared to v3
* Well-funded & proven contributors

**Cons**
* Almost everything is configurable (and needs to be configured)
* Initial setup is quite intensive
* Basic stuff like CSS modules doesn't work out of the box
* Not all documentation and plugins are ready for v4

<div align="center">
<br>
<br>
<img alt="Parcel" src="https://user-images.githubusercontent.com/19409/31321658-f6aed0f2-ac3d-11e7-8100-1587e676e0ec.png" width="749">
<br>
<br>
</div>

#### Setup the build using Parcel Bundler
blabla

* Create `.postcss` file `{"modules": true}` in the root dir
* Create an entry point `index.js` / `index.html`
* run `parcel <entry-point>`
* Optional: create a `tsconfig.json` file for the TypeScript configuration

**Pros**
* Very quick to setup
* For most projects this is a plug-n-play solution
* Built in dev server
* Very fast compile times
* `index.html` as entry point

**Cons**
* Configuration / cusomization is required to write a plugin
* Losts of magic is going on in the background
* Small community still
* Have to prove itself future proof

### Takeaway
webpack -> safe choice, less risks


Parcel is great to setup new projects fast. This can be very helpfull for R&D or PoC purposes. It might be a good fit to replace Webpack but it has to prove that it can survive next to Webpack. At least until Webpack 5 is released, there is a much better developer experience with Parcel than with Webpack. But Webpack 5 will have a lot more features that will enable 0CJS like built-in support for CSS modules.
