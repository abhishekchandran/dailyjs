---
layout: post
title: "Node Roundup: 0.10, Versions, cors"
author: "Alex Young"
categories: 
- node
- modules
- middleware
- servers
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a>.
</div>

###Node 0.10.0

It's finally here!  [Node 0.10.0](http://blog.nodejs.org/2013/03/11/node-v0-10-0-stable/) has been released, which means your custom streams can now be rewritten with the new primitive classes.  This is a good thing.  The announcement post has a lot of details on benchmarks, and mentions the new [Node CI server](http://jenkins.nodejs.org/) that shows the build status for each of the platforms Node officially supports.

> ... all streams in Node-core are built using the same set of easily-extended base classes, so their behavior is much more consistent, and it's easier than ever to create streaming interfaces in your own userland programs.

Isaac mentions 37 modules are using the [readable-stream](https://github.com/isaacs/readable-stream) module.  This module allows _streams2_ to be used with Node 0.8 applications, so you can use it as a bridge to migrate older code.  There are also _streams2_ modules already out there -- for example, [tub](https://npmjs.org/package/tub) by Eirik Albrigtsen uses the new `Transform` class.

The road to 1.0.0 will see a Node 0.12 series released first.  The goal of 0.12 will be to improve Node's HTTP implementation, which will involve improving the encapsulation between client and server code and reworking the socket pooling behaviour.

###Versions

Versions (GitHub: [3rd-Eden / versions](https://github.com/3rd-Eden/versions), License: _MIT_, npm: [versions](https://npmjs.org/package/versions)) by Arnout Kazemier is a module for creating a content delivery network.  It was designed to address performance concerns when using Node for serving static assets when compared to servers that support [`sendfile` like Nginx](http://wiki.nginx.org/HttpCoreModule#sendfile).  It does things like sets the correct HTTP caching headers, and has a REST API for server management which also outputs various metrics.

Arnout wrote a great introduction to Versions, [Versions: The Node.js Content Delivery Network](http://blog.nodejitsu.com/content-delivery-network-in-node-js), which explains how to configure the application as well as demonstrating the improvements it offers.

###cors

cors (GitHub: [TroyGoode / node-cors](https://github.com/TroyGoode/node-cors), License: _MIT_, npm: [cors](https://npmjs.org/package/cors)) by Troy Goode is Express/Connect middleware for working with cross-origin resource sharing.  This allows your Express apps to accept cross-origin requests by writing out the appropriate HTTP headers.

The readme includes an asynchronous example that illustrates how to conditionally accept requests.  You could use it to whitelist specific domains for apps that are configured for multiple domains.
