---
layout: post
title: "Node Roundup: Node-sass, TowTruck, peer-vnc"
author: "Alex Young"
categories: 
- node
- modules
- sass
- css
- vnc
- mozilla
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a>.
</div>

###Node-sass

Node-sass (GitHub: [andrew / node-sass](https://github.com/andrew/node-sass), License: _MIT_, npm: [node-sass](https://npmjs.org/package/node-sass)) by Andrew Nesbitt is a Node binding for libsass.  It comes with some pre-compiled binaries, so it should be easy to get it running.

It has both synchronous and asynchronous APIs, and there's an example app built with Connect so you can see how the middleware works: [andrew / node-sass-example](https://github.com/andrew/node-sass-example).

{% highlight javascript %}
var sass = require('node-sass');
// Async
sass.render(scss_content, callback [, options]);

// Sync
var css = sass.renderSync(scss_content [, options]);
{% endhighlight %}

The project includes Mocha tests and more usage information in the readme.

###TowTruck

[C. Scott Ananian]( http://cscott.net) sent in [TowTruck](http://towtruck.mozillalabs.com/) (GitHub: [mozilla / towtruck](https://github.com/mozilla/towtruck), License: _MPL_) from Mozilla, which is an open source web service for collaboration:

> Using TowTruck two people can interact on the same page, seeing each other's cursors, edits, and browsing a site together. The TowTruck service is included by the web site owner, and a web site can customize and configure aspects of TowTruck's behavior on the site.

It's not currently distributed as a module on npm, so you'll need to follow the instructions in the readme to install it.  There's also a bookmarklet for adding TowTruck to any page, and a Firefox add-on as well.

###peer-vnc

peer-vnc (GitHub: [InstantWebP2P / peer-vnc](https://github.com/InstantWebP2P/peer-vnc), License: _MIT_, npm: [peer-vnc](https://npmjs.org/package/peer-vnc)) by Tom Zhou is a web VNC client.  It uses his other project, [iWebPP.io](https://github.com/InstantWebP2P/iwebpp.io), which is a P2P web service module.

I had trouble installing node-httpp on a Mac, so YMMV, but I like the idea of a P2P [noVNC](http://kanaka.github.io/noVNC/) project.
