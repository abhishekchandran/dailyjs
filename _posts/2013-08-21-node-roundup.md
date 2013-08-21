---
layout: post
title: "Node Roundup: 0.10.16, ungit, image-size"
author: "Alex Young"
categories: 
- node
- modules
- git
- apps
- images
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a>.
</div>

###Node 0.10.16

[Node 0.10.16](http://blog.nodejs.org/2013/08/16/node-v0-10-16-stable/) has been released, which includes an update for npm, and fixes for the crypto, http, and stream modules.

###ungit

![ungit logo](/images/posts/ungit.png)

ungit (GitHub: [FredrikNoren / ungit](https://github.com/FredrikNoren/ungit), License: _MIT_, npm: [ungit](https://npmjs.org/package/ungit)) is a web-based UI for Git, written with Node.  It makes Git repositories easier to visualise, a bit like `gitk` or `git instaweb`, but it has some GitHub-specific tweaks.

![ungit repo](/images/posts/ungit-repo.png)

It can be installed with `npm install -g ungit`, and is run with `ungit` on the command-line.  You can set up an `.ungitrc` which is a JSON file that currently just changes the port.

Once you're running ungit, you can make commits, discard them, fetch remote changes -- pretty much the standard Git operations you're used to, with a friendlier workflow.

###image-size

If you need to get image sizes without using command-line binaries, then take a look at image-size (GitHub: [netroy / image-size](https://github.com/netroy/image-size), License: _MIT_, npm: [image-size](https://npmjs.org/package/image-size)) by Aditya.  It looks at the relevant bits in a file by using a Node buffer, and supports popular formats like PNG, GIF, BMP, and even PSD.

It has an asynchronous and synchronous API:

{% highlight javascript %}
var sizeOf = require('image-size');
sizeOf('images/example.png', function(err, dimensions) {
  console.log(dimensions.width, dimensions.height);
});
{% endhighlight %}
