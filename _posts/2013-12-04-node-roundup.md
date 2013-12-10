---
layout: post
title: "Node Roundup: Ben Noordhuis, Node.app, Infect.js"
author: Alex Young
categories:
- node
- modules
- objective-c
- di
---

###Ben Noordhuis

Every time I write about a new Node release, I notice how much work Ben Noordhuis has done.  He's been an important contributor to Node and libuv, and has always seemed patient and polite on the mailing list.

[Ben Noordhuis decided to leave Node and libuv](http://blog.nodejs.org/2013/12/03/bnoordhuis-departure/).  If you're not familiar with his work, take a look at the [Node ChangeLog](https://github.com/joyent/node/blob/master/ChangeLog) -- Ben's commits go back to summer 2010.  Ben will be missed!

###Node.app

![Node.app](/images/posts/nodeapp.png)

[Node.app](http://nodeapp.org/) (GitHub: [node-app / Interpreter](https://github.com/node-app/Interpreter), License: _MIT_) is a project to bring Node's API to JavaScriptCore.  The aim is a drop-in replacement that's compatible with Node's master branch, and to reuse the JavaScript in Node's `lib/` directory (the core modules).

It needs the latest iOS or Mac OS X, and if you check out the source you'll need to get the submodules (`git submodule update --init --recursive`).

The list of currently working modules includes partial `fs` support, `util`, `url`, `events`, `path`, `stream`, `querystring`, and `assert`.  The `process` object is also supported.

I've only had a brief look at the source in [node-app / Nodelike](https://github.com/node-app/Nodelike/), but it looks like they're writing Objective-C to add the necessary libuv bindings.  This is the code you'll find in `src/` in [joyent / node](https://github.com/joyent/node).

###Infect.js

[Infect.js](http://blog.amwmedia.com/post/66879608871/infect-js-infectiously-simple-dependency-injection) (GitHub: [amwmedia / infect.js](https://github.com/amwmedia/infect.js), License: _MIT_, npm: [infect](https://npmjs.org/package/infect)) by Andrew Worcester is a dependency injection module.  It's not specifically for Node, but I was intrigued by the idea of bringing AngularJS-style DI to Node projects.

> Registering a dependency.  A simple call to `infect.set()` with the name you want to use, and the mutable object you'd like to register will do the trick. In the example below we are using a function, but you can register any type of mutable value (Functions, Arrays, Objects, etc).

{% highlight javascript %}
infect.set('Logger', function(str) {
  // prepend a time to every log line
  console.log((new Date()).toLocaleTimeString() + ' ==> ' + str);
});
{% endhighlight %}

It supports function injection (`infect.func`) and class injection (`infect.func` with a constructor function).  Andrew has included jsFiddle examples in the readme, so you can play around with the code.

