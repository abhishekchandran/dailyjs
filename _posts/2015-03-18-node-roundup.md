---
layout: post
title: "Node Roundup: 0.10.37 and io.js 1.5.1, Node and Real-time Finance, comws"
author: Alex Young
categories:
- node
- modules
- libraries
- generators
- articles
---

###0.10.37 and io.js 1.5.1

[Node 0.10.37](http://blog.nodejs.org/2015/03/14/node-v0-10-37-stable/) was released on Saturday.  This updates uv, domains, buffer, console, v8, and http.  The uv update fixes a [security issue](https://bugzilla.redhat.com/show_bug.cgi?id=1194651) which allowed attackers to gain elevated privileges due to the way `setuid` and `setgid` were used.

[io.js 1.5.1](https://medium.com/node-js-javascript/io-js-week-of-march-13th-e3024cc66802) also came out last week.  The blog post has some useful community updates, including a talk by Tony Pujals about [the future of io.js](https://vimeo.com/121707989).

There's also an [npm weekly post](http://blog.npmjs.org/post/113882628280/npm-weekly-9) about fixes for `npm shrinkwrap --dev`, changes to `shrinkwrap` in npm 3, and a screencast by Ben Clinkinbeard about using npm link.

###Node and Real-time Finance

Imre Fazekas sent in two articles about Node and real-time finance:

* [Part 1](http://blog.upwardsmotion.com/nodejs-in-the-enterprise-world-the-building-infrastructure/)
* [Part 2](http://blog.upwardsmotion.com/nodejs-in-the-enterprise-world-the-building-infrastructure-part-2/)

The first part covers the background and architecture of the project, and the second part goes into the build system.  It sounds like the third part will expand on client/server code sharing, so presumably it'll feature some of the author's experiences with isomorphic templates and view models.

###Comws

What if you like Koa's generator-based middleware but don't want to use Koa?  Andrea Parodi has created Comws (GitHub: [shes/comws](https://github.com/shes/comws), License: _MIT_, npm: [comws](https://www.npmjs.com/package/comws)), a library based on [co](https://github.com/tj/co) that you can use with any Node application.

To use it, create an instance of `CoMws` and then add generators to the middleware stack:

{% highlight javascript %}
var CoMws = require('comws');
var mws = new CoMws();

mws.use(function *(next){
  this.result += ' hello';
  yield next();
});

mws.use(function *(next){
  this.result += ' world';
  yield next();
});

var ctx = { result: 'yet another' };

mws.run(ctx).then(function() {
  //ctx.result === 'yet another hello world' 
});
{% endhighlight %}

If you're using Node 0.10.x you'll need to run it with `--harmony-generators` or `--harmony`, but Node 0.12 and io.js should work without the flags.

I'd like to try this with Express, but it also seems like a useful module for non-web Node programs.
