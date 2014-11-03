---
layout: post
title: "McFly, React Widgets, react-separate-template"
author: "Alex Young"
image: "/images/posts/reactwidgets.png"
categories:
- react
- reactive
- widgets
- ui
---

###McFly

[McFly](http://kenwheeler.github.io/mcfly/) (GitHub: [kenwheeler/mcfly](https://github.com/kenwheeler/mcfly), License: _BSD_) by Ken Wheeler is a Flux implementation.  It uses Facebook's Dispatcher, and provides factories for Actions and Stores.

To use McFly, create an instance of `McFly` then make a store with `mcFly.createStore`.  You can then generate new actions with `mcFly.createActions`.

Internally, CommonJS modules are used with a Browserify-based build script to generate the final browser-friendly source, so it's modular and easy to read.

###React Widgets

If you need some UI widgets for your React projects, then you might want to try [React Widgets](http://jquense.github.io/react-widgets/docs/) (GitHub: [jquense/react-widgets](https://github.com/jquense/react-widgets), License: _MIT_, npm: [react-widgets](https://www.npmjs.org/package/react-widgets)) by Jason Quense.  It's influenced by jQuery UI and Kendo UI, and implements dropdown lists, combo boxes, selects, datetime pickers, and a calendar.

The usage is based on custom elements with attributes that set up the data binding to drive the widgets.  Each widget has several attributes that provide a good level of flexibility, and they support keyboard shortcuts as well.

###Separating React Templates

Sergii Kliuchnyk wanted to keep React HTML fragments in separate files to make it easier to work on stylesheets without building part or all of an application.  [react-separate-template](https://github.com/redexp/react-separate-template) is a GitHub repository that explores this idea.

There's a script called [conv.js](https://github.com/redexp/react-separate-template/blob/master/conv.js) that combines a JavaScript file with a corresponding HTML file to make the resulting `.jsx` file that you'd usually find in a React project.

There are still some issues, like the handling of attributes, but it seems like something that could be adapted to work as part of a typical Gulp/Grunt build script.
