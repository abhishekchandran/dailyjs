---
layout: post
title: "Cytoscape.js"
author: "Alex Young"
categories: 
- libraries
- node
- maths
---

![Cytoscape](/images/posts/cytoscape.png)

[Cytoscape.js](http://cytoscape.github.io/cytoscape.js/) (GitHub: [cytoscape / cytoscape.js](https://github.com/cytoscape/cytoscape.js), License: _LGPL_, npm: [cytoscape](https://npmjs.org/package/cytoscape)), developed at the Donnelly Centre at the University of Toronto by Max Franz, is a graph library that works with Node and browsers.  This library is for working with "graphs" in the mathematical sense -- interconnected sets of nodes connected by edges.

The API uses lots of sensible JavaScript idioms: it's event-based, functions return objects so calls can be chained, JSON definitions of elements can be used, and nodes can be selected with selectors that are modelled on CSS selectors and jQuery's API.  That means you can query a graph with something like this: `cy.elements('node:locked, edge:selected')`.

Styling graphs is also handled in a natural manner:

> Graph style and data should be separate, and the library should provide core functionality with extensions adding functionality on top of the library.

Max and several contributs have been working on the project for [two years now](https://github.com/cytoscape/cytoscape.js/tree/ccb76539fb2cdcdaff8ee799b7faeda89d48f484), so it's quite mature at this point.  The project comes with detailed documentation, a build script, and a test suite written with QUnit.
