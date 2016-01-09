## What is Polymer?
Polymer is a lean & light library from Google that pushes the next evolution of the web.
It adds elegance in building custom DOM/html elements, while providing less boilerplate code.
## Goals
- Decrease Development Friction with tools
- Use polygit & bower for managing elements.  There's an element for that!
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


1. "Blank page rabbithole effect" : 
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