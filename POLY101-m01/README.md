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