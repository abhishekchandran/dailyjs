---
layout: post
title: "Node Roundup: 0.11.2, 0.10.6, subscribe, Omelette"
author: "Alex Young"
categories: 
- node
- modules
- cli
- events
- pubsub
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a>.
</div>

###Node 0.11.2 and 0.10.6

Clearly the Node core developers have had an early summer holiday, and are now back to unleash new releases.  In the space of a few days [0.11.2](http://blog.nodejs.org/2013/05/13/node-v0-11-2-unstable/) and [0.10.6](http://blog.nodejs.org/2013/05/14/node-v0-10-6-stable/) were released.  I was intrigued by the `Readable.prototype.wrap` update, which makes it support `objectMode` for streams that emit objects rather than strings or other data.

The 0.11.2 release has an update that guarantees the order of `'finish'` events, and another that adds some new methods: `cork` and `uncork`.  Corking basically forces buffering of all writes -- data will be flushed when `uncork` is called or when `end` is called.

There is a detailed discussion about `cork` and the related `_writev` method on the Node Google Group: [Streams writev API](https://groups.google.com/d/msg/nodejs/UNWhF64KeQI/zN2VCWYkMhcJ).  There are some interesting comments about a similar earlier implementation by Ryan Dahl, the validity of which Isaac questions due to Node's code changing significantly since then.

If you want to read about `writev`, check out the `write(2)` (`man 2 write`) manual page:

> `Write()` attempts to write `nbyte` of data to the object referenced by the descriptor `fildes` from the buffer pointed to by `buf`.  `Writev()` performs the same action, but gathers the output data from the `iovcnt` buffers specified by the members of the `iov` array...

###subscribe

Azer Koçulu has been working on a suite of modules for subscribing and observing to changes on objects:

* Watch for changes to arrays: [watch-array](https://github.com/azer/watch-array)
* Watch for changes to objects: [new-object](https://github.com/azer/new-object)
* Array-like pub/sub: [new-list](https://github.com/azer/new-list)

Now he's also released a module for [subscribing](https://github.com/azer/pubsub) to multiple pub/sub objects:

{% highlight javascript %}
var subscribe = require('subscribe');
var a = pubsub();
var b = pubsub();
var c = pubsub();

subscribe(a, b, c, function(updates) {
  updates[0].pubsub;
  // => a.onUpdate
  updates[0].params;
  // => 3, 4
  updates[1].pubsub;
  // => c.onUpdate
  updates[1].params;
  // => 5, 6
});

a.publish(3, 4);
c.publish(5, 6);
{% endhighlight %}

This brings a _compositional_ style of working to Azer's other modules, allowing subscriptions to multiple lists and objects at the same time.  The next example uses subscribe to combine the new-list module with new-object:

{% highlight javascript %}
var fruits = newList('apple', 'banana', 'grapes');
var people = newObject({ smith: 21, joe: 23 });

subscribe(fruits, people, function(updates) {
  updates[0].params[0].add;
  // => melon

  updates[1].params[1].set;
  // => { alex: 25 }
});

fruits.push('melon');
people('alex', '25');
{% endhighlight %}

###Omelette

Omelette (GitHub: [f / omelette](https://github.com/f/omelette), License: _MIT_, npm: [omelette](https://npmjs.org/package/omelette)) by Fatih Kadir Akın is a template-based autocompletion module.

Programs and their arguments are defined using an event-based completion API, and then they can generate the zsh or Bash completion rules.  There's an animated gif in the readme that illustrates how it works in practice.

