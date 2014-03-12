---
layout: post
title: "Node Roundup: 0.11.12, Metalsmith, Promises and Error Handling"
author: Alex Young
categories:
- node
- modules
- npm
- promises
- generators
---

<div class="intro">
  <strong>Job ad</strong>: <a href="https://iridize.com/">Iridize</a> is looking for a <a href="http://dailyjs.com/iridize.html">lead frontend developer</a>.
</div>

###Node 0.11.12

[Node 0.11.12](http://blog.nodejs.org/2014/03/12/node-v0-11-12-unstable/) is out.  It updates uv, some of Node's C++ code in `src/`, and several core modules including cluster and net.

One commit that caught my attention was [buffer: allow toString to accept Infinity for end](https://github.com/joyent/node/pull/7281) by Brian White.  He said he sometimes sets `INSPECT_MAX_BYTES` to `Infinity`, allowing the buffer's contents to be printed for debugging purposes.  I think it's interesting that this works, even though it's not something I'd usually want to do.

###Metalsmith

[Ian Storm Taylor](http://ianstormtaylor.com/) sent in [Metalsmith](http://www.metalsmith.io/), a really cool static site generator by [Segment.io](https://segment.io/).  Why is it cool?  Well, they had me at the entirely plugin-based API that uses chainable calls:

{% highlight javascript %}
Metalsmith(__dirname)
  .use(drafts())
  .use(markdown())
  .use(permalinks('posts/:title'))
  .use(templates('handlebars'))
  .build();
{% endhighlight %}

###Promises and Error Handling

[Promises and Error Handling](http://making.change.org/post/69613524472/promises-and-error-handling) by Jon Merrifield is all about error handling with promises in Node.  It has guidelines for using promises safely, including the idea that you should reject rather than `throw` and how to terminate chains early and safely.

> Changing the `then` in the above code to `done` means that there will be no outer promise returned from this, and the error will result in an asynchronous uncaught exception, which will bring down the Node process. In theory this makes it unlikely that any such problem would make it into production, given how loudly and clearly it would fail during development and testing.

