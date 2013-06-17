---
layout: post
title: "Data.IO, CoffyScript, Circular Progress"
author: Alex Young
categories: 
- browser
- libraries
- ES6
- coffeescript
- Canvas
---

###Data.IO

Data.IO (GitHub: [scttnlsn / data.io](https://github.com/scttnlsn/data.io), License: _MIT_, npm: [data.io](https://npmjs.org/package/data.io)) by Scott Nelson is a library for bidirectional syncing over Socket.IO.  It has server-side resources which encapsulate logic and persistence.  Resources are stacks of composable middleware functions that sync client requests.  The client-side component is comparatively lightweight -- it's lower-level than Backbone.js, so I suspect it could be used with any data binding library.

Data.IO allows you to keep core business logic on the server, while easily subscribing to data in the client.  It's a bit like Backbone.js and Express, but purpose-built for working with data syncing.

###CoffyScript

CoffyScript (GitHub: [loveencounterflow / coffy-script](https://github.com/loveencounterflow/coffy-script)) by "loveencounterflow" is a port of CoffeeScript that adds support for `yield` from ES6:

> If you have never programmed with iterators and generators, you may imagine as a 'resumable return' for starters. For the more technically oriented, ES6 defines generators as "First-class coroutines, represented as objects encapsulating suspended execution contexts (i.e., function activations)." Well, maybe 'resumable return' is not so bad after all.

{% highlight coffeescript %}
# Using a star after the arrow 'licenses' the use of `yield` in the function body;
# it basically says: this is not an ordinary function, this is a generator function:
count = ->*
  yield 1
  yield 2
  yield 3

# Calling a generator function returns a generator:
counting_generator = count()

# Now that we have a generator, we can call one of its methods, `next`:
log counting_generator.next()   # prints: { value: 1, done: false }

# ...and we can go on doing so until the generator becomes exhausted:
log counting_generator.next()   # prints: { value: 2, done: false }
log counting_generator.next()   # prints: { value: 3, done: false }
log counting_generator.next()   # prints: { value: undefined, done: true }
log counting_generator.next()   # throws an error saying "Generator has already finished"
{% endhighlight %}

The documentation in the readme is thorough, and explores various aspects of working with `yield`.  For example: [How Not to Yield to Callback Hell: Serializing Control Flow](https://github.com/loveencounterflow/coffy-script#how-not-to-yield-to-callback-hell-serializing-control-flow).

###Circular Progress

![Circular Progress](/images/posts/circular-progress.png)

Circular Progress (GitHub: [neoziro / circular-progress](https://github.com/neoziro/circular-progress), License: _MIT_, bower: _circular-progress_) by Greg Bergé is a progress widget with no dependencies.  Given a Canvas element, it'll show a circular representation of a process's progress:

{% highlight javascript %}
var progress = new CircularProgress({
  radius: 70,
  strokeStyle: 'black',
  lineCap: 'round',
  lineWidth: 4
});

document.body.appendChild(progress.el);
progress.update(40);
{% endhighlight %}

