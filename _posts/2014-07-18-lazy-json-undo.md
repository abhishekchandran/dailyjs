---
layout: post
title: "Undo with Object.observe"
author: "Alex Young"
categories:
- libraries
- browser
- dom
---

Polgár András sent in LazyJsonUndoRedo (GitHub: [azazdeaz / LazyJsonUndoRedo](https://github.com/azazdeaz/LazyJsonUndoRedo), npm: [lazy-json-undo-redo](https://www.npmjs.org/package/lazy-json-undo-redo), Bower: _LazyJsonUndoRedo_), which uses ES6's `Object.observe` to bless undo and redo support on arbitrary JavaScript objects.  That means if you've got a rich UI component you can add intuitive undo support.

[There's a demo](http://codepen.io/azazdeaz/pen/AEgGe?editors=001) that shows a graphical maze which supports undo and redo that illustrates the concept nicely.  It sets the maze's `map` object to use LazyJsonUndoRedo, and whitelists some special objects:

{% highlight javascript %}
var ljur = new LazyJsonUndoRedo();
ljur.setWhitelist(map, ['data', 'objectMap', 'objectData', 'width', 
  'height', 'name', 'gridSize', 'showGrid', 'showWalls']);
ljur.observeTree(map);

var gui = new dat.GUI();
gui.add({ undo: function() { ljur.undo(); } }, 'undo');
gui.add({ redo: function() { ljur.redo(); } }, 'redo');
{% endhighlight %}

`Object.observe` is supported in the latest stable Chrome, and there's a Polymer shim for older browsers.  The shim should work in IE 9 and above.

Internally, LazyJsonUndoRedo uses an array to store changes and a pointer so objects can be fetched as required.

