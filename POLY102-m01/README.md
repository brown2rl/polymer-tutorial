## Creating an element with starter kit

1. Download and the Full Intermediate Starter Kit and its dependancies from the link in 101.  Alternatively,
```
$ git clone https://github.com/polymerelements/polymer-starter-kit.git
```
3. install bower components in the new directory
```
$ bower install
```
4. move bower_components to /app (otherwise gulp will not build correctly)
```
$ mv bower_components app
```
2. check to see that the fresh installation is served correctly (using Chrome). if you need to change ports, go to ```node_modules/browser-sync/lib/default-config.js``` and change from 3001 (Polymer Starter Kit)
```
$ gulp && gulp serve
```
3. here's the breakdown of the project directory/starter kit:

- app/ is where you store all of your source code and do all of your development.
- elements/ is where you keep your custom elements.
- images/ is for static images.
- scripts/ is the place for JS scripts.
- styles/ houses your app’s shared styles and CSS rules.
- test/ is where you define tests for your web components.
- docs/ contains optional “recipes” (how-to guides) for adding features to your application or for using optional tools or editors.
- dist/ is the directory to deploy to production. When you run the build task, files are prepared for production (HTML imports are vulcanzied, scripts are minimized, and so on) and output to this directory.-