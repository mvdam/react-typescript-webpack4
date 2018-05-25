## Parcel Bundler versus webpack 4
> Setting up a fresh TypeScript React project

Starting up a new project can be quite intensive. Most time will vanish in setting up the build process. We all know the pains of setting up Webpack with loaders and configuration files. But things might have changed. We have two -new- kids on the block;

* Parcel Bundler (released December, 2017)
* webpack 4 (released on Februari, 2018)

### #0CJS
...

### App requirements

Before going any further, lets determine some requirements for our application. When thinking of a professional app, we should at least have support for the following technology.
- [ ] React
- [ ] TypeScript (TSX)
- [ ] Being able to import
    - JavaScript modules (obviously)
    - CSS Modules
    - Fonts
    - Images
- [ ] Dev server

Steps needed for it to run;

Parcel
* Create `.postcss` file `{"modules": true}` in the root dir
* Create an entry point `index.js` / `index.html`
* run `parcel <entry-point>`
* Optional: create a `tsconfig.json` file for the TypeScript configuration

webpack 4
* Create `webpack.config.js` file
* Configure loaders for TypeScript, CSS modules, Fonts and images
* Configure dist folder
* Create an entry point `index.js`
* For production build support we also need to configure source maps and `ExtractTextPlugin` to be able to bundle all the CSS
* Configure dev server with HMR
* Run `webpack`
* Optional: create a `tsconfig.json` file for the TypeScript configuration



<notes>
Only 0CJS from webpack 5 (css modules support)



Parcel
Pro
* Very quick to setup
* For most projects this is a plug-n-play solution
* Built in dev server
* Very fast compile times

Cons
* Configuration / cusomization is required to write a plugin
* Losts of magic is going on in the background
* Small community still
* Have to prove itself future proof


webpack 4
Pros
* Almost everything is configurable
* Large community
* Greatly improved compilation speed compared to v3
* Well-funded & proven contributors

Cons
* Almost everything is configurable (and needs to be configured)
* Initial setup is quite intensive
* Basic stuff like CSS modules doesn't work out of the box
* Not all documentation and plugins are ready for v4


Takeaway
Parcel is great to setup new projects fast. This can be very helpfull for R&D or PoC purposes. It might be a good fit to replace Webpack but it has to prove that it can survive next to Webpack. At least until webpack 5 is released, there is a much better developer experience with Parcel than with webpack. But webpack 5 will have a lot more features that will enable 0CJS like built-in support for CSS modules.