---
layout: post
title: "AngularJS D3 Charts, Yo three.js, TinyCore.js"
author: Alex Young
categories:
- libraries
- webgl
- architecture
- graphics
- yeoman
---

###AngularJS D3 Charts

Chinmay sent in [Angular-charts](http://chinmaymk.github.io/angular-charts/) (GitHub: [chinmaymk / angular-charts](https://github.com/chinmaymk/angular-charts), License: _MIT_, bower: _angular-charts_), a set of AngularJS directives for graphs that use D3.  To use it, include `angular-charts.min.js` and then inject the dependency with `angular.module('yourApp', ['angularCharts'])`.

Configuration options for graphs can be included using directives, or passed as options in JavaScript.  There are also events for `mouseover`, `mouseout`, and `click`.  The charts have animations, tooltips, and the values will be adapted to the graph's size as necessary.

###A Yeoman Generator for three.js

If you're looking for a friendly way to get started with three.js, then Timmy Willison's [Yeoman generator](http://timmywillison.com/post/68797881874/a-yeoman-generator-for-three-js) (GitHub: [timmywil / generator-threejs](https://github.com/timmywil/generator-threejs), License: _MIT_, npm: [generator-threejs](https://npmjs.org/package/generator-threejs)) may be what you're looking for.

The template it outputs renders a red cube, and it includes the usual Yeoman stuff like a Grunt build script and a web server for development.

###TinyCore.js

TinyCore.js (GitHub: [mawrkus / tinycore](https://github.com/mawrkus/tinycore), License: _MIT_) by Marc Mignonsin is a library for organising projects around modules:

> We use dependency injection to provide the modules the tools they need to perform their job. Instead of having a single sandbox object with a lot of methods, a module defines explicitly the tools it needs. The mediator, that provides a way of communication for the modules, is one of the default tools that has already been implemented (located in the "tools/mediator" folder).

Modules have an extensible, event-based API.  There's also a factory class, called "Toolbox":

> In order to provide the modules the tools they need to perform their job, TinyCore uses a tools factory, `TinyCore.Toolbox`.
> A tool can be registered at any time for later use. Whenever a module is instantiated, the tools specified in the module definition will be requested and injected as parameters of the creator function.

TinyCore is written with testing in mind, and has an extension for Jasmine.
