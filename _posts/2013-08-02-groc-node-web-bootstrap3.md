---
layout: post
title: "Bootstrap 3, Node Web Development, Groc"
author: Alex Young
categories:
- node
- books
- bootstrap
- documentation
---

###Bootstrap 3

<div class="image">
  <img src="/images/posts/bootstrap3.png" alt="" />
  <small>Bootstrap 3's homepage.</small>
</div>

[Bootstrap 3 RC1](http://blog.getbootstrap.com/2013/07/27/bootstrap-3-rc1/) is out, and you'll see Bootstrap 3 on the front page of [getbootstrap.com](http://getbootstrap.com/):

> With over ~1,600 commits, ~72,000 additions/deletions, and ~300 files changed, everything has changed. We've added features, removed features, and cleaned up a lot more. The v3 pull request on GitHub has all the details you'll need for a complete list of changes and some helpful migration tips.

Before you get too excited you should know that it'll take some work to migrate to Bootstrap 3.  There's no magic migration button as far as I know.  Grids still scale up to 12 columns, but now use the class prefix `.col-`.  Forms have different classes and tweaked markup, but the newer markup seems better to me.  I don't think we need `<div class="controls">` anymore, for example.

###Node Web Development - Second Edition

[Node Web Development - Second Edition](http://www.packtpub.com/node-web-development-2e/book) has been released, written by [David Herron ](http://nodejs.davidherron.com/).

He's written a post about it [on his blog](http://nodejs.davidherron.com/2013/07/node-web-development-2nd-edition-has.html):

> The final version of the sample application includes user authentication support, the ability to work with multiple database engines, be deployed on cloud services, and it dynamically sends data back and forth between server and browser to dynamically update the screen when other people edit things, and to support sending little messages between users of the application.

###Groc

In [Rock Your Doc With Groc, Our Favorite Automated Frontend Documentation Tool](http://tech.gilt.com/post/57089759513/rock-your-doc-with-groc-our-favorite-automated), [a fork of Groc](http://nevir.github.io/groc/) is discussed which adds support for tags:

> We just couldn’t find a tool that gave us everything we needed. In the end, we created our own automated documentation tool by forking Docco and adding (hacking) support for Tags.

Groc, by Ian MacLeod, is a fork of [docco](http://jashkenas.github.io/docco/) by Jeremy Ashkenas.  The post on Gilt's blog does a good job of explaining why they need tags and how they use them.
