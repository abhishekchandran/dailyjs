---
layout: post
title: "Morearty.js, ngDroplet"
author: "Alex Young"
image: "/images/posts/ngdroplet.png"
categories:
- angularjs
- react
- libraries
---

###Morearty.js

Marat Bektimirov sent in Morearty.js (GitHub: [moreartyjs / moreartyjs](https://github.com/moreartyjs/moreartyjs), License: _Apache 2.0_, npm: [morearty](https://www.npmjs.org/package/morearty)), a state management library inspired by [Om](https://github.com/swannodette/om).  It's based on the immutable data structures in [immutable.js](https://github.com/facebook/immutable-js) -- the idea is components and subcomponents only have access to a nested version of data that is synchronised with the original binding.  That means each component only knows what it should, which should improve encapsulation within the application.

> Morearty detects any changes automatically and triggers re-rendering. Each component gets a correctly defined `shouldComponentUpdate` method that compares the component's state using straightforward JavaScript strict equals operator `===.` So, only the components whose state was altered are re-rendered.

This might sound similar to [Omniscient.js](http://omniscientjs.github.io/), which I wrote about recently.  Omniscient could technically work with other immutable libraries, but is similar to Morearty.  Libraries like these help you focus on generic state change operations so you don't get too bogged down in DOM structure.

Morearty's binding methods return `this`, so you should be able to chain calls.  It comes with tests and has high test coverage.

###ngDroplet

[ngDroplet](http://ng-droplet.herokuapp.com/) (GitHub: [Wildhoney / ngDroplet](https://github.com/Wildhoney/ngDroplet), License: _MIT_, Bower: `ng-droplet`) by Adam Timberlake is a new HTML5 file uploading library for Angular that supports drag and drop and image previews.  You can set the allowed extensions and show upload progress if your server sends the `X-File-Size` header.

It uses the custom `droplet` element or a `data-droplet` attribute, and it uses a `DropletModel` object that contains the metadata for selected files.
