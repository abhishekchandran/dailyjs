---
layout: post
title: "AngularCollection, datamock.js, store.js"
author: Alex Young
categories: 
- mvc
- angularjs
- testing
- databases
- localStorage
---

###AngularCollection

AngularCollection (GitHub: [tomkuk / angular-collection](https://github.com/tomkuk/angular-collection), License: _MIT_, bower: _angular-collection_) by Tomasz Kuklis is a collection module for AngularJS.  It allows objects to be added, removed, updated, and fetched at a specific index.  It also has a `sort` method and `last`.

It comes with a Grunt build script and some unit tests.

###datamock.js

[datamock.js](http://marksteve.com/datamock.js/) (GitHub: [marksteve / datamock.js](https://github.com/marksteve/datamock.js), License: _MIT_) by Mark Steve Samson is a small library for generating sample data for mockups.  Data attributes can be used to bind mocked data, like this: `<p data-mock="lorem">Lorem ipsum here...</p>`.

It includes some other value types, like names and emails.  The author has included a `bookmarklet` task in the build script so you can generate a bookmarklet that fills a page in with test sample data.

###store.js

store.js (GitHub: [nbubna / store](https://github.com/nbubna/store), License: _MIT_) by Nathan Bubna is a friendlier API for localStorage and sessionStorage.  Basic usage is `store(key, data)`, but it has other functions like `store.setAll`, `store.getAll`, and support for namespaces.

The sessionStorage API is accessed through `store.session`, for example: `store.session(key, 'value')`.  The project includes a Grunt build script and PhantomJS-powered tests.
