---
layout: post
title: "Node Roundup: 0.8.19, 0.9.9, Peer Dependencies, hapi, node-treap"
author: "Alex Young"
categories: 
- node
- modules
- frameworks
- web
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a>.
</div>

###Node 0.8.19, 0.9.9, and Peer Dependencies

[Node 0.8.19 was released last week](http://blog.nodejs.org/2013/02/06/node-v0-8-19-stable/) and this version includes an update for npm that supports [peer dependencies](http://blog.nodejs.org/2013/02/07/peer-dependencies/).  I'm excited about this feature, and I'll be interested to see how it pans out over time.  Basically, you can now specify dependencies for "plugins". Think jQuery plugins, or in a Node project Grunt plugins are a good example.

This will require plugin authors to update their `package.json` files with a `peerDependencies` property, but it should make managing things like Express middleware and Grunt easier in the future.  I already find npm's dependency management relatively stress-free, and this seems like a step in the right direction.

Also, Node [0.9.9](http://blog.nodejs.org/2013/02/07/node-v0-9-9-unstable/) was also released last week, which now features a streams2-powered tls module.

###hapi

![hapi](/images/posts/hapinode.png)

[hapi](http://walmartlabs.github.com/hapi/) (GitHub: [walmartlabs / hapi](https://github.com/walmartlabs/hapi), License: [LICENSE](https://github.com/walmartlabs/hapi/blob/master/LICENSE), npm: [hapi](https://npmjs.org/package/hapi)) from Walmart Labs is a framework for building RESTful API services.  There are already a few solid RESTful API modules for Node (like [restify](http://mcavage.github.com/node-restify/)), so hapi looks to be building on that concept rather than being an MVC web framework.

There's a basic example that provides an overview of the API:

{% highlight javascript %}
var Hapi = require('hapi');

// Create a server with a host, port, and options
var server = new Hapi.Server('localhost', 8080);

// Define the route
var hello = {
  handler: function(request) {
    request.reply({ greeting: 'hello world' });
  }
};

// Add the route
server.addRoute({
  method : 'GET',
  path : '/hello',
  config : hello
});

// Start the server
server.start();
{% endhighlight %}

Gone is the `req, res` pattern (which comes from Node's core modules, not Connect).  The [hapi API documentation is extremely detailed](https://github.com/walmartlabs/hapi/blob/master/docs/Reference.md), and includes examples for the main features.  The routing API does seem extremely flexible, but it's hard to judge it without seeing a large hapi application.

[hapi, a Prologue](http://hueniverse.com/2012/12/hapi-a-prologue/) by Eran Hammer is a detailed post that compares hapi to Express, which is useful if you're familiar with Express. Eran writes:

> We also had some bad experience with Express' lack of true extensibility model. Express was a pleasure and easy to use 2 years ago with a limited set of middleware and very little interdependencies among them. But with a long list of chained middleware, we found hard to debug problems when we simply changed the order in which middleware modules were being loaded.

I've always thought the answer to this was to make smaller, interconnected services.  Rather than a large Express application with complex middleware, shouldn't we be using multiple Express applications that communicate with each other?  Technically Express could be a veneer on top of a more complex architecture.

Eran brings up other points as well, but it's difficult to say how well hapi or Express satisfy the goals of building large production web applications because people building things at that level don't release gory details about their solutions to architectural problems.  I occasionally run into a friend who works on a Rails project with _thousands_ of models.  It doesn't work very well.  But where are concrete details on real solutions to the problem of scaling business logic?

###node-treap

node-treap (GitHub: [brenden / node-treap](https://github.com/brenden/node-treap), License: _MIT_, npm: [treap](https://npmjs.org/package/treap)) by Brenden Kokoszka is a [Treap](http://en.wikipedia.org/wiki/Treap) implementation.  A treap is a self-balanced binary search tree.  Once a tree has been created, keys can be added with data objects:

{% highlight javascript %}
var treap = require('treap');
var t = treap.create();

// Insert some keys, augmented with data fields
t.insert(5, { foo: 12 });
t.insert(2, { foo: 8 });
t.insert(7, { foo: 1000 });
{% endhighlight %}

Then elements can be fetched and removed:

{% highlight javascript %}
var a = t.find(5);
t.remove(a); // by reference to node
t.remove(7); // by key
{% endhighlight %}

Brenden has included tests, and each API method has documentation in the readme.  He's included some notes on what treaps are, so you don't need to be fresh off the back of a computer science degree to figure out what the module does.

