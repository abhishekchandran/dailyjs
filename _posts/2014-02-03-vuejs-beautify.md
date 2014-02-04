---
layout: post
title: "Vue.js, beautify-with-words"
author: Alex Young
categories:
- node
- modules
- mvvm
- mvc
---

###Vue.js

![Vue.js](/images/posts/vuejs.png)

[Vue.js](http://vuejs.org/) (GitHub: [yyx990803 / vue](https://github.com/yyx990803/vue), License: _MIT_) by Evan You is a MVVM library.  It's based around instances of the `Vue` constructor, essentially view model objects, that provide bindings between DOM objects and data models.

It has an event-based API with key/value observing, HTML directives (like AngularJS), and text filters.  There's a [TodoMVC example](https://github.com/yyx990803/vue/tree/master/examples/todomvc) that showcases some of the features.  Most of the code is passed in as options to the `Vue` constructor, so it feels a little bit like Backbone.js views in that respect.

Vue.js is an interesting combination of features from Backbone.js, KnockoutJS, and AngularJS.  Evan seems confident about its performance and features, but I think it'll be hard to convince people to seriously try it out given how popular Backbone and AngularJS have become.

###beautify-with-words

beautify-with-words (GitHub: [zertosh / beautify-with-words](https://github.com/zertosh/beautify-with-words), License: _MIT_, npm: [beautify-with-words](https://npmjs.org/package/beautify-with-words)) by Andres Suarez is a module based on UglifyJS that replaces variable names with words.

You can pass `-b` to beautify the output, which essentially means you can turn minified, obfuscated code into something not quite readable, but much easier to search and grep for patterns.

