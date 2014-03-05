---
layout: post
title: "Node Roundup: npm Trademark, Cha"
author: Alex Young
categories:
- node
- modules
- npm
---

###Charlie Robbins and the npm Trademark

Charlie Robbins, who you may know as [indexzero](https://github.com/indexzero), recently published [An open letter to the Node community](http://blog.nodejitsu.com/an-open-letter-to-the-node-community/):

> Being part of a community means listening to it. After listening to the deep concern that has been voiced over our application to register the npm trademark we have decided to withdraw the application from the USPTO. I want to apologize for the way that our message came across. We hastily reacted to something that clearly needed more thought behind it.

[Nodejitsu previously announced](https://blog.nodejitsu.com/protecting-npm/) its intention of registering the npm trademark, and although it seems like it was with the best intentions, the confusion that arose was understandable.

Charlie signs off the post by saying the Node community needs a non-profit "foundation" that helps manage Node:

> There is little beyond GitHub issues and discussions as to the questions like roadmap and long term plans. A non-profit organization could get more of this tedious work done by having more dedicated resources instead of relying on individual community members to go it alone.

Many of us have seen something similar happen in companies we've worked at: we use GitHub issues and small, informal groups to manage things quite happily until the business grows and management mistakes become more dangerous.

Recently we've seen the arrival of npm, Inc and [TJ Fontaine take over Node](http://blog.nodejs.org/2014/01/16/nodejs-road-ahead/), so things are changing.  I'm not sure how a non-profit Node Foundation fits into this, but as someone who depends on Node for his career I think Charlie has raised some important questions that need addressing.

###Cha

![Cha](/images/posts/chajs.png)

Cha (GitHub: [chajs / cha](https://github.com/chajs/cha), License: _MIT_, npm: [cha](https://www.npmjs.org/package/cha)) is a module for defining tasks and chaining them together.  It can be used to define build scripts, or whatever else you'd like to automate, and the author shows how to tie them to npm `scripts` as well.

This is what the basic API looks like:

{% highlight javascript %}
var cha = require('../')

// Set a watcher.
cha.watch = require('./tasks/watch')

cha.in('read', require('./tasks/read'))
   .in('cat', require('./tasks/cat'))
   .in('coffee', require('./tasks/coffee'))
   .in('write', require('./tasks/write'))
   .in('uglifyjs', require('./tasks/uglifyjs'))
   .in('copy', require('./tasks/copy'))
{% endhighlight %}

There is a [specification for tasks](https://github.com/taskjs/spec), and it allows text-based "expressions" to be defined that can glob files and do other cool stuff with less syntax:

{% highlight javascript %}
cha(['glob:./fixtures/js/*.js', 'request:http://underscorejs.org/underscore-min.js'])
{% endhighlight %}

