---
layout: post
title: "Node Roundup: 0.9.8, Queen, AssetViz"
author: "Alex Young"
categories: 
- node
- modules
- graphics
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a>.
</div>

###0.9.8

[Node 0.9.8](http://blog.nodejs.org/2013/01/24/node-v0-9-8-unstable/) is out.  This release includes an interesting patch from Jake Verbaten to [support arbitrary objects in streams](https://github.com/joyent/node/commit/444bbd4fa7315423a6b55aba0e0c12ea6534b2cb).  Internally, streams now switch to `objectMode` when objects are detected.  The unit tests illustrate how this works in practice:

{% highlight javascript %}
test('can read objects from stream', function(t) {
  var r = fromArray([{ one: '1'}, { two: '2' }]);
  var v1 = r.read();
  var v2 = r.read();
  var v3 = r.read();

  assert.deepEqual(v1, { one: '1' });
  assert.deepEqual(v2, { two: '2' });
  assert.deepEqual(v3, null);
  t.end();
});
{% endhighlight %}

Notice how each `read` causes an object to be returned.  Jake has been heavily involved with streams over the last year or two, with plenty of notable modules in his [Raynos GitHub account](https://github.com/Raynos?tab=repositories).

###Queen

![Queen](/images/posts/queen.png)

Last week I wrote about Ozan Turgut's [Thrill](http://thrilljs.com/) project.  The core component, which people seemed to find more interesting, was [Queen](http://queenjs.com/) (GitHub: [turn / queen](https://github.com/turn/queen), License: _Apache v2_, npm: [queen](https://npmjs.org/package/queen)).  Queen is a server that can run scripts on multiple browsers.  This could be used for anything, not just for running tests which is what Thrill does.

Queen clients and servers have bidirectional communication, and Queen will detect and recover unresponsive browsers.  It can target browsers by type, version, and OS, and run scripts via the command-line.

###AssetViz

![AssetViz on DailyJS](/images/posts/assetviz.png)

AssetViz (GitHub: [Munter / assetviz](https://github.com/Munter/assetviz), License: _MIT_, npm: [assetviz](https://npmjs.org/package/assetviz)) by Peter Müller is a _command-line web application source code visualisation tool_.  It generates self-contained HTML files that show a visualisation of the site using D3.js.

The nodes that make up the visualisation can be dragged and will spring back into place, and you can also zoom using the mousewheel.
