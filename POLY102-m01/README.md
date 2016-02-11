## setting up

1. Download and the Full Intermediate Starter Kit and its dependancies from the link in 101.  Alternatively,
```
$ git clone https://github.com/polymerelements/polymer-starter-kit.git
```
3. install bower components in the new directory
```
$ bower install
```
4. make sure bower_components is in app/ (otherwise gulp will not build correctly)

5. check to see that the fresh installation is served correctly (using Chrome). if you need to change ports, go to ```node_modules/browser-sync/lib/default-config.js``` and change from 3001 (for browserSync UI) and ```project/gulpfile.js``` from 5001 (line 220 for PSK UI)
```
$ gulp && gulp serve
```
6. if all goes well, you should have an output that looks like this:
![PSK initial output](PSK_initial_page.png)

7. here's the breakdown of the project directory/starter kit.. it's the larger system in which we will integrate our custom element:

- app/ is where you store all of your source code and do all of your development.
- elements/ is where you keep your custom elements.
- images/ is for static images.
- scripts/ is the place for JS scripts.
- styles/ houses your app’s shared styles and CSS rules.
- test/ is where you define tests for your web components.
- docs/ contains optional “recipes” (how-to guides) for adding features to your application or for using optional tools or editors.
- dist/ is the directory to deploy to production. When you run the build task, files are prepared for production (HTML imports are vulcanzied, scripts are minimized, and so on) and output to this directory.

## creating our element
In order to create our custom element, we're going to utilize the seed element and polyserve.
The seed element gives us the ablity to create and test reusable elements with a localized version of Polymer in order 
to integrate it into the larger system. It also allows us to create API documentation on the fly.
### setting up
1. download/unzip or clone [the seed element](https://www.polymer-project.org/1.0/docs/start/reusableelements.html) into app/elements
2. install polyserve globally ```npm install -g polyserve```
3. ```bower install``` for your components (may have to include them in demo and test)
4. run ```polyserve``` or ```polyserve -p 9999``` if you need a different port (for C9 users, be sure to ```polyserve -H 0.0.0.0```)
5. if all goes well, you should see a landing page looking like the following:
![reusable element output](reusable-element.png)

![reusable element demo](reusable-element-demo-.png)
### adding some better stuff
- open seed-element.html from ```project/seed-element```
- we're going to remove the contents of the element, and add a button to represent restarting a particular device
- lets start by deleting the contents of ```<style></style>``` and ```<template></template>``` so that the HTML looks like (without ```<script></script>```)
```
<link rel="import" href="../polymer/polymer.html">
<link rel="import" href="../paper-fab/paper-fab.html">
<link rel="import" href="../iron-icons/notification-icons.html">

<!--
An element representing the restart signal for a device

Example:

    <seed-element></seed-element>

@demo
-->
<dom-module id="seed-element">

  <style>
    paper-fab {
      --paper-fab-background: orange; // init & rebooting state
    }
  </style>

  <template>
    <paper-fab icon="notification:power"></paper-fab>
  
  </template>

</dom-module>
```
- next, we'll open up the contents of ```project/seed-element/demo/index.html```.  this is what is displayed when we click "demo" at the top right after we serve the page
- notice the assignment in the ```author``` custom attribute is an object that is passed to the Polymer function in ```seed-element.html```
- remove the extraneos stuff in the ```<body>```, ```<seed-element>```, and ```<script>``` so that we only have the following:
```
<html>
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, minimum-scale=1.0, initial-scale=1.0, user-scalable=yes">
    <title>seed-element Demo</title>
    <script src="../../webcomponentsjs/webcomponents-lite.js"></script>
    <link rel="import" href="../seed-element.html">
  </head>
  <body>

    <seed-element>
      
    </seed-element>

    <script>
 
    </script>

  </body>
</html>
```
- now, when we run ```polyserve``` and click demo, we get something looking like
![demo-element-power-button](power-button-demo.png)
---
data binding video inspiration: [data binding vid](https://youtu.be/1sx6YNn58OQ)


- parses HTML for {{}} child component -> parent component data and [[]] parent component -> child component data and makes property effects
- $0._propertyEffects to inspect property effects in chrome
- gets ```set function() {}``` in ```Polymer({})``` for:
	 "dirty checking" ( data value diffing & chacing )
	 running property effects
	 listeining to changed events
- _setFoo = private setter
- setting readonly

