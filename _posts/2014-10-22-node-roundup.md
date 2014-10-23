---
layout: post
title: "Node Roundup: npm's Registry Architecture, Mongeese, Synaptic"
author: "Alex Young"
image: "/images/posts/synaptic.png"
categories:
- modules
- libraries
- node
- ai
- database
- mongodb
---

###npm's Registry Architecture

npm's blog has a post about the [registry's roadmap](http://blog.npmjs.org/post/100099402720/registry-roadmap) for the second phase of its architectural development.  This post has some interesting stats about the amount of traffic npm gets, and how the design is changing to make it scale up.

The new design is based around modular microservices, so it follows the trends employed by other large scale services.

> We call this collection of changes "Registry 2". It will resolve some lingering inefficiency in the existing architecture and give us even more room to scale, but more importantly it will allow us to add a bunch of new features. We're very, very confident that it will work, because it's already in production: npm Enterprise already uses this architecture, and the Registry 2 project is largely a matter of taking this architecture and scaling it up.

The cool thing about this is it means npm will be able to offer private packages -- these are invisible packages that only your collaborators can see.  The post points out that using lots of small packages is the "Node way", but npm doesn't currently help us achieve that due to the reliance on public packages.

The way I get around the lack of private packages is to host private modules on GitHub with an OAuth2 token in the URL.  I find this approach better than Git submodules, but it lacks the ability to easily control what version of a package is included so it's not really suitable for deployments that I don't have complete control over.

> But if you write code that is closed-source, or is just too specific to your own application to make a good public module, your options right now are full of friction and split-brain thinking. Why can't you just npm publish and npm install all the private packages in your app, the same way you can with public packages? People kept asking us to make it possible to do this, so we did.

This should be released in early 2015.  You can register for the beta using a form in the blog post.

I don't know if private packages or "npm for teams" will be mean npm is going to offer subscription plans, but I expect to see subscriptions for some functionality next year.  I don't have a problem with that, as a long paying GitHub subscriber, but the post doesn't seem to mention anything about paid plans.  Of course, there is already [npm Enterprise](https://www.npmjs.org/enterprise), but this is different from ad-hoc collaboration.

###Mongeese

Mongeese (GitHub: [zekenie / mongeese](https://github.com/zekenie/mongeese), License: _ISC_, npm: [mongeese-array](https://www.npmjs.org/package/mongeese-array)) by Zeke Nierenberg modifies Mongoose to make the Array class include extra async methods, including `asyncEach`, `asyncMap`, and `asyncReduce`.  Here's an example of `asyncMap`:

{% highlight javascript %}
var iterator = function(oneKitten, done) {
  done(null, oneKitten.name)
};

someUser.kittens.asyncMap(iterator, function(err, kittenNames) {
  // kitten names -> ['fluffy', 'cuddles', ...]
});
{% endhighlight %}

It works by using the `async` module and `lodash`.  Because it modifies Mongoose it may cause issues with future API changes, but you may like it if you use a lot of arrays.

###Synaptic

[Synaptic](http://synaptic.juancazala.com/index.html) (GitHub: [cazala / synaptic](https://github.com/cazala/synaptic), License: _MIT_, npm: [synaptic](https://www.npmjs.org/package/synaptic)) by Juan Cazala is a neural network library.  There are some cool demos, like [an image filter based on training a perceptron](http://synaptic.juancazala.com/filter.html).

> This library includes a few built-in architectures like multilayer perceptrons, multilayer long-short term memory networks (LSTM) or liquid state machines, and a trainer capable of training any given network, which includes built-in training tasks/tests like solving an XOR, completing a Distracted Sequence Recall task or an Embeded Reber Grammar test, so you can easily test and compare the performance of different architectures.

The readme explains what each of the module's classes do, to the extent that it reads like an introduction to neural networks.  It also has some powerful features, like being able to export a network as a single JavaScript function, so you can use trained networks without any dependencies.
