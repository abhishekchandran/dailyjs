---
layout: post
title: "App.net Node Module, Prototype 1.7.1, Self, Qwerty Hancock, MilkChart"
author: Alex Young
categories: 
- libraries
- node
- browser
- audio
- social
- prototype
- graphs
---

###App.net Node Module

There's already an [App.net](https://join.app.net/) Node module: [damienklinnert / appdotnet](https://github.com/damienklinnert/appdotnet) (License: _MIT_, npm: [appdotnet](https://npmjs.org/package/appdotnet).  Created by Damien Klinnert, it uses the popular [request HTTP module](https://npmjs.org/package/request), and has Mocha tests.  It supports authentication, users, and posts.

Creating a post is very simple:

{% highlight javascript %}
client.createPost(config.post_data, function(err, post) {
  // Do something with `post`
});
{% endhighlight %}

###Prototype 1.7.1

(SFX: Simple Minds - Alive And Kicking)

[Prototype 1.7.1](http://prototypejs.org/2012/8/8/prototype-1-7-1) has been released, which includes a rewrite of the DOM code, ECMAScript 5 compatibility, as well as other bug fixes.

> Many of you have wondered whether Prototype is "dead," and I can say that it definitely isn't. But because of the way I work on Prototype - months of inaction followed by a flurry of commits and bug fixes - it's fair to say that Prototype hibernates for long periods of time.

###Self

[Self](https://github.com/munro/self) (License: _MIT_, npm: [self](https://npmjs.org/package/self)) by Ryan Munro is a class library based on Python.  It supports inheritance, mixins, static properties, and can work with plain old prototype classes and Backbone.

> Self is class-based sugar that's perfect for continuation-passing style. No more `var that = this;`! The implicit `this` variable is changed to an explicit self variable that your inner functions inherit. Self plays nicely with existing prototypal, and Backbone OOP.

Self can be used with browsers and in Node programs, and includes tests for both environments.

###Qwerty Hancock

![Query Hancock](/images/posts/qwertyhancock.png)

[Qwerty Hancock](http://stuartmemo.com/qwerty-hancock/) (GitHub: [stuartmemo / qwerty-hancock](https://github.com/stuartmemo/qwerty-hancock), License: _MIT_) by Stuart Memo is a "vector qwerty keyboard".  The project's site demonstrates the keyboard by hooking it up to some Audio API code, so it's actually a reusable keyboard widget that could be used to build other music-related projects.

###MilkChart

[MilkChart](https://github.com/theiviaxx/MilkChart) (License: _MIT_) by Brett Dixon is a graph library for MooTools.  It generates graphs that look like Excel.  It's designed to transform HTML tables into charts, so it's easy to integrate it with existing markup that requires graphs.
