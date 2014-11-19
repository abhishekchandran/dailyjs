---
layout: post
title: "Node Roundup: Taunus, Root Path, Mongorito"
author: "Alex Young"
image: "/images/posts/taunus.png"
categories:
- node
- libraries
- modules
- google
- frameworks
---

###Taunus

![Taunus](/images/posts/taunus.png)

[Taunus](http://taunus.bevacqua.io/) (GitHub: [taunus/taunus](https://github.com/taunus/taunus), License: _MIT_, npm: [taunus](https://www.npmjs.org/package/taunus)) by Nicolas Bevacqua is an MVC framework that offers full-stack progressive enhancement.  It uses server-side rendering, and will also use the browser's history API for routing if it's available.

> Taunus can deal with view caching on your behalf, if you so desire, using asynchronous embedded database stores on the client-side. Turns out, there's pretty good browser support for IndexedDB. Of course, IndexedDB will only be used if it's available, and if it's not then views won't be cached in the client-side besides an in-memory store. The site won't simply roll over and die, though.

It supports both Hapi and Express, so there's some flexibility on the server.  The server-side component is mainly dedicated to rendering.

There's a [getting started guide](http://taunus.bevacqua.io/getting-started) that shows how to set up a Taunus project and how to do basic things like adding a layout.

###Root Path

Chris Morrell wrote a [detailed response to a StackOverflow question](https://stackoverflow.com/questions/10265798/determine-project-root-from-a-running-node-js-application/18721515#18721515) about finding the root path for a Node project.

This resulted in the App Root Path Module (GitHub: [inxilpro/node-app-root-path](https://github.com/inxilpro/node-app-root-path), License: _MIT_, npm: [app-root-path](https://www.npmjs.org/package/app-root-path)), a small module that returns the path to the current module's main directory.  It returns a string, so you just have to do `require('app-root-path')` and pass the output to `require`.

Chris notes that the basic method for this is: `path.resolve(__dirname).split('/node_modules')[0];`, but there are edge cases where `require.main.filename` is used instead.  This is all explained in the StackOverflow post.

###Mongorito for ES6

If you're using an ES6-based HTTP framework like [Koa](http://koajs.com/), then you might feel your database library could do with generator support as well.  Fortunately, Vadim Demedes has rewritten his MongoDB module, [Mongorito](http://mongorito.com/) (GitHub: [vdemedes/mongorito](https://github.com/vdemedes/mongorito), License: _MIT_, npm: [mongorito](https://www.npmjs.org/package/mongorito)) to use ES6 generators.

Now you can load items like this:

{% highlight javascript %}
var posts = yield Post.find();
{% endhighlight %}

Saving works the same way:

{% highlight javascript %}
yield post.save(); // document created

var id = post.get('_id'); // _id automatically had been set after .save()
{% endhighlight %}

It's based on the [monk](https://github.com/Automattic/monk) MongoDB module, and has good test coverage.  I've never used a module like this in production, but I definitely like the idea of generator syntax for databases.
