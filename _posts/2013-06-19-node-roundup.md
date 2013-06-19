---
layout: post
title: "Node Roundup: Node 0.10.12, grunt-micro, connect-prerenderer"
author: "Alex Young"
categories: 
- node
- modules
- cluster
- grunt
- connect
- express
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a>.
</div>

###Node 0.10.12

[Node 0.10.12](http://blog.nodejs.org/2013/06/18/node-v0-10-12-stable/) was released yesterday.  This version updates v8 and npm, and has a fix for the net module.

One minor change that I liked was readline now supports `CTRL-L` for clearing the screen -- that means Node's command-line interface will do this as well.  Before hitting `CTRL-L` did nothing, which wasn't very intuitive if you're used to using readline tools.

###grunt-micro

If size is important to you, then you'll like grunt-micro (GitHub: [markdalgleish / grunt-micro](https://github.com/markdalgleish/grunt-micro), License: _MIT_, npm: [grunt-micro](https://npmjs.org/package/grunt-micro)) by Mark Dalgleish.  This Grunt plugin ensures a script is smaller than a given size.  Mark suggests this is useful for client-side authors that have size claims in their project documentation, but it could be useful for other things, like warning about asset sizes in mobile projects.

###connect-prerenderer

connect-prerenderer (GitHub: [dai-shi / connect-prerenderer](https://github.com/dai-shi/connect-prerenderer), License: _BSD_, npm: [connect-prerenderer](https://npmjs.org/package/connect-prerenderer)) by Daishi Kato is middleware for pre-rendering content to support systems that don't interact well with Ajax-heavy interfaces.  This is ideal for improving the SEO of a site.

The author has paid special attention to AngularJS -- the documentation includes some Angular client-side code that adds support for the module.
