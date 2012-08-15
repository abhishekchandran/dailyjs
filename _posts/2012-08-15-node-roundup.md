---
layout: post
title: "Node Roundup: Surviving npm Downtime, Waf Wall of Shame, stream-chat, Vein"
author: "Alex Young"
categories: 
- node
- modules
- RPC
- WebSocket
- npm
- templating
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###Surviving npm Downtime

On Sunday morning (UTC) part of npm's service stopped functioning correctly, which meant the command-line tool failed to download packages.  In response to this, [Dominique Sandoz](https://twitter.com/streunerlein) stepped up and created a mirror.  Mirrors can be used by changing the location of the npm registry:

{% highlight javascript %}
npm set registry http://npm.example.com
npm set registry https://registry.npmjs.org
{% endhighlight %}

Fortunately npm is now working correctly, but to help prepare for future downtime I recommend bookmarking this gist that Dominique wrote containing a list of [npm mirrors and proxies](https://gist.github.com/3332181).

During the downtime, several other users also offered their own solutions, mostly collaborating on Twitter and IRC.  For example, Maciej Małecki [created a proxy-based solution](https://twitter.com/maciejmalecki/status/234640793476947970).

To my knowledge there has been no official statement on the service outage, and additionally there is no official Node/npm service status page.  Hopefully someone will write up details about the outage on [blog.nodejs.org](http://blog.nodejs.org/), and outline the preventative measures taken to ensure future stability.

###Node-waf Wall of Shame

Isaac Schlueter posted a Tweet referencing what he calls the "Node-waf wall of shame":

> Node-waf wall of shame: [http://j.mp/node-waf-users](http://t.co/hoANsgtz)  Upgrade your packages to node-gyp. [http://npm.im/node-gyp](http://npm.im/node-gyp)  #deathtowaf

As I mentioned in the [Windows and Node](http://dailyjs.com/2012/05/17/windows-and-node-3/) series, it's time to move addons over to [node-gyp](https://github.com/TooTallNate/node-gyp).

###stream-chat

[stream-chat](https://github.com/Raynos/stream-chat) (License: _MIT_) by Raynos is a chat app based around [streams](http://nodejs.org/docs/latest/api/all.html#all_stream).  It uses the [boot](https://github.com/Raynos/boot) and [multi-channel-mdm](https://github.com/Raynos/multi-channel-mdm) modules by the same author to route streams between browsers and Node servers.

An added bonus is the author has designed the chat app to be scalable by using [seaport](https://github.com/substack/seaport) and [mountie](https://github.com/substack/mountie) by James Halliday.  Seaport helps manage clusters of servers, while mountie allows applications to be composed of smaller servers behind mount points.  Routing is handled by [bouncy](https://github.com/substack/bouncy).  These modules help design larger systems according to the concept of [separation of concerns](http://en.wikipedia.org/wiki/Separation_of_concerns), which suits Node web applications.

###MinnaHTML.js

[MinnaHTML.js](https://github.com/RobeeeJay/MinnaHTML.js) (License: _GPL v3_, npm: [minnahtml](https://npmjs.org/package/minnahtml)) by Robee Shepherd is an async-friendly HTML object library that can be used to build HTML:

{% highlight javascript %}
var mh = require('minnahtml').mh
  , html = new mh.Html()
  , head = new mh.Head(html)
  ;

 new mh.Title(head).data.content = 'Example';
 
 console.log(html.generateHtml());

// <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
// <html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en">
//  <head>
//   <title>
//    Example
//   </title>
//  </head>
// </html>
{% endhighlight %}

The author has provided a walkthrough that covers more features in the project's readme file.

###Vein

[Vein](https://github.com/wearefractal/vein) (License: _MIT_, npm: [vein](https://npmjs.org/package/vein)) is a WebSocket RPC module.  It includes both client and server code, and a minimised build for browsers.  RPC methods can be added using `vein.add`, and then called from clients:

{% highlight javascript %}
// Server
vein.add('multiply', function(res, numOne, numTwo) {
  res.reply(numOne * numTwo);
});

// Browser
var vein = Vein.createClient();
vein.on('ready', function(services) {
  vein.multiply(2, 5, function(num) {
    // num === 10
  });
});
{% endhighlight %}
