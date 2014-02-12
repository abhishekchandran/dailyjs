---
layout: post
title: "Node Roundup: Multiple Node Instances, to-locals, pipes-and-filters"
author: Alex Young
categories:
- node
- modules
- apps
---

###Running Multiple Instances in a Single Process

StrongLoop has a useful blog with lots of posts about Node.  Yesterday Ben Noordhuis posted [Running Multiple Instances in a Single Process](http://strongloop.com/strongblog/whats-new-node-js-v0-12-multiple-context-execution/):

> Imagine a node-webkit application where each window runs its own Node instance that is isolated from all other windows. Or Node embedded in a phone or network switch where it is performing routing logic for multiple connections, but in a single process.

> It's a pretty tall order because Node started out as – and still is – a single-threaded application, built around the concept of a single event loop, with hundreds of global variables that store various bits of state.

The post goes on to show how add-on authors can use contexts, with `NODE_MODULE_CONTEXT_AWARE`.

###to-locals

eyy sent in to-locals (GitHub: [eyy / to-locals](https://github.com/eyy/to-locals), License: _MIT_, npm: [to-locals](https://www.npmjs.org/package/to-locals)), a module that transforms callback functions into Connect middleware that automatically sets `res.local` for use in views.  This example shows how easy it is to expose Mongoose models:

{% highlight javascript %}
var users = toLocals(mongoose.model('users'), 'find', 'users');
app.get('users', users, function(req, res, next) {
  // res.locals now has the loaded users
});
{% endhighlight %}

It's a small project, but even so Mocha tests have been included, and the documentation highlights the main features.

###Pipes and Filters

Pipes and Filters (GitHub: [slashdotdash / node-pipes-and-filters](https://github.com/slashdotdash/node-pipes-and-filters), License: _MIT_, npm: [pipes-and-filters](https://www.npmjs.org/package/pipes-and-filters)) by Ben Smith is a module for composing sets of asynchronous operations:

{% highlight javascript %}
Pipeline.create('order processing')
  .use(decrypt)
  .use(authenticate)
  .use(deDuplicate)
  .breakIf(function(input) { return input.exists; })
  .execute(message, function completed(err, result) {
    // error or success handler
  });
{% endhighlight %}

Ben wrote a blog post that introduces the module with detailed examples: [Pipes and Filters to cure Node.js async woes](http://10consulting.com/2014/02/11/pipes-and-filters-to-cure-node-async-woes/).

> How can we perform complex processing on an input data structure, while maintaining independence and flexibility?

> The Pipes and Filters pattern provides one possible solution. Described in the Enterprise Integration Patterns book as a method to "divide a larger processing task into a sequence of smaller, independent processing steps (Filters) that are connected by channels (Pipes)."

