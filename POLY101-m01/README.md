## What is Polymer?
Polymer is a lean & light library from Google that pushes the next evolution of the web.
It adds elegance in building custom DOM/html elements, while providing less boilerplate code.
## Goals
- Decrease Development Friction with tools
- Use polygit & bower for managing elements.  "There's an element for that!"
- "Every byte has a cost" mantra
- Using polylint for error management
- Achieving great performance by using polydev to mesure the efficiency of the elements
- http/2
- building complex apps with DOM as a framework-oriented carbon elements

## Thinking in Polymer
- using the Document Object Model as a framework
- using custom html elements as components for ease & interoperability
1. think locally by examining 1 element at a time
2. use composition to build custom element in private implementation / shadowDOM
3. use mediator pattern using parent/host element as mediator and API as language: > The essence of the Mediator Pattern is to define an object that encapsulates how a set of objects interact.  Objects no longer communicate directly with each other, but instead communicate through the mediator.
- some basic syntax:
`<dom-module id="parent/host-element-name">`

## End to End w/ polymer (idea to production)
Some common problems : solutions:


1. Avoiding "Blank page rabbithole effect" : 
  - use [Polymer Starter Kit](https://developers.google.com/web/tools/polymer-starter-kit/?hl=en)!  It comes bundled with elements & Gulp for deployment.
  - use [NPM yeoman generator package](https://www.npmjs.com/package/generator-polymer-gulp) (`npm install generator-polymer-gulp -g`, then `yo polymer && gulp serve`) for easy starter kit install!
2. Breaking up the app :
  - break down to smaller components/elements (modularize!)
  - container->view->data strucure->data item
  - an example script.. 
```
<dom-module id="container_name">
	<script>
		Polymer({
			is: 'container_name',
			properties: {
				data_item: {
					notify: true, // 2-way bindable
					value: function(){
						return [ // data_items are objects in an array
							{
								label: 'data_item label'
								isComplete: false // a flag
							},
							_
						];
					}
				}
			}
		});
	</script>
</dom-module>
```
  - then use data bindings & reference your element..
```
<dom-module id="view_name">
	<template>
		<data_strutcure_name data_item="{{data_item}}"></data_structure_name>
	</template>
	<script>
		Polymer({
			is: 'view_name',
			properties: {
				data_item: Array // binds data to data_structure_name element
			}
		});
	</script>
</dom-module>
```
```
 <body>
 	<template is="dom-bind">
	 <container_name data_item="{{data_item}}"></container_name>
	 <view_name data_item="{{data_item}}"></view_name>
	</template>
</body>
```

##Testing
 - Web Component Tester (WCT): Mocha, Chai, & Sinon.
 - tests should be written to avoid "state leak":
 1. should be order independant
 2. should be runnable in isolation
 3. should be consistenly repeatable
 - we use the `<text-fixture>` element to help
 - example:
 ```
 <head>
 	<title> paper button tests </title>
	<script src="../../web-component-tester/browser.js"></script>
	
	<link rel="import" href="../paper-button-html">
</head>
<body>
<!-- HTML Test Fixtures (can add as many fixutres as you want)-->
	<test-fixture id="PaperButton">
		<template>
			<paper-button> Test Button </paper-button>
		</template>
	</test-fixture>
	
<!-- Test Suite -->
	<script>
		suite('paper-button, function() { //setting test
			var button;
			
			//using <test-fixture> to avaoid global state leakage
			setup( function (){
				button = fixture('PaperButton'); // from mocha
				
				/**
				 stubs from sinon give the ability to 
				 change how functions are called without changing the
				 subject element, <paper-button>
				**/
				stub('paper-button', {
					click: function() {
						console.log('PaperButton.click called!');
						
						// some expect() statements..
						
						}					
				});
				
				/**
				We can also replace an element with a fake one in the
				DOM and	run expectations on the fake one for the 
				duration of the test
				**/
				replace('paper-button).with('fake-paper-button');
				
				/**
				Accessibility (a11y) fixture testing using the Chrome 
				Accessibility Developer Tools extension
				**/
				a11ySuite('PaperButton');
			});
		
			test('for the win', function () { // applying test
				//what to expect by grabbing button
				expect(document.querySelector('paper-button')).to.be.ok;
			});
		});
	</script>
</body>
```
 - run `wct` in current working directory for all browser tests

##Platinum Elements set
- great for client side networking
Offline:
- offline = removing a dependency from a network
- control the offline experience.. create your own offline dinosaur game!
Service Worker:
- control the interaction with the server
- stores Req/Res pairs in a local cache
- ex:
```
<platinum-sw-register auto-register>
	<!-- handle route requests -->
	<platinum-sw-fetch path="/images/(.*)"
	handler="networkFirst">
	</platinum-sw-fetch>
	
	<!-- define the cache resource -->
	<platinum-sw-cache default-cache-strategy="networkFirst"
	precache='["index.html',"main.css"]'>
	</platinum-sw-cache>
</platinum-sw-register>
```
- cache strategies (when resource fetching fails):
1. networkOnly - sw doesn't do anything
2. networkFirst - look in cache if nothing from server
3. cacheFirst - load from cache first, then server if not found
4. fastest - go to both cache and server and use whatever loads fastest
5. custom - for profiling and configuring different geo regions
- can create user-defined caching
Messaging:
- prompting for notfication in context of the app
- push notifications/messaging
- example:
```
<platinum-push-messaging
	title="A push message"
	body="Disable this push message?"
	image="gear-icon.png"
	click-url="/settings"
	message-url="/settings.json">
</platinum-push-messaging>
<toggle-button></toggle-button>
```
- event example:
```
var ppm =
	document.querySelector('platinum-push-messaging');

toggle.addEventListner('click',
	e => toggle.checked ? ppm.enable() : ppm.disable());
	
ppm.addEventListner('subsription-changed',
	e => sendSubscription(ppm.subscription));
```
Device Access (Limited ChromeOS)
- example device element:
```
<platinum-bluetooth-device 
	id="device"
	services-filter='["heart-rate"]'>
	
		<platinum-bluetooth-characteristic
			id="fitbit"
			service="heart-rate"
			characteristic="body-sensor-location"
			value={{bodySensorLocation}}>
		</platinum-bluetooth-characteristic>
</platinum-bluetooth-device>
<span>{{bodySensorLocation}}</span>
<script>
var device = document.querySelector('#device'); //getting device object

var fitbit = document.querySelector(#fitbit');

//request the device access
device.request();
//read device data on approval
char.read();
```