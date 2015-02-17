---
layout: post
title: "Wallaby, React and Node at the BBC"
author: Alex Young
image: "http://wallabyjs.com/assets/img/inline.png"
categories:
- react
- node
- libraries
- bbc
- sponsored-content
- testing
---

###Wallaby

<div class="sponsored-content" style="background-color: #f0f4cf; padding: 0; margin: 10px 0; border-radius: 5px; font-size: 90%; width: 530px; padding: 0 1px">
  <p><a class="label" href="/sponsored-content.html">Sponsored Content</a> This post is about a commercial product that we think will appeal to DailyJS readers.</p>
</div>

<img src="/images/posts/wallaby.gif" style="width: 530px" />

[Wallaby.js](http://wallabyjs.com/) is a continuous test runner that outputs results directly into your editor.  It includes code coverage, so you'll get a visual indication of blocks of code that aren't tested.  It also uses dependency analysis to only run tests affected by changes, and runs tests in parallel to improve performance.

The supported editors include:

* WebStorm
* IntelliJ IDEA Ultimate
* PhpStorm
* RubyMine
* PyCharm Professional

The authors are working on Visual Studio support as well.

The following screenshot shows the line covering test feature:

<img src="http://wallabyjs.com/assets/img/inline.png" style="width: 530px" />

There's [an example project](https://github.com/wallabyjs/public) that you can use to see how Wallaby works in practice.

Wallaby currently supports PhantomJS, and plans to support Node and io.js. The developers are working on supporting compile-to-JavaScript languages like TypeScript, CoffeeScript, and React JSX.

The project is commercial but is currently free to try out.  Wallaby's creator, Artem Govorov, has written a blog post about [the motivation behind starting the project](http://dm.gl/2015/01/30/wallaby/).

###The New BBC Homepage

If you're overwhelmed by JavaScript frameworks, then you might be interested to hear about the BBC's new homepage, which has been built with React, Express, and Node.  There's a detailed post about it by Andrew Hillel: [How we built the new BBC Homepage](http://www.bbc.co.uk/blogs/internet/entries/47a96d23-ae04-444e-808f-678e6809765d).

> This allows us to serve more simultaneous requests, increasing the performance of the application. As a result, we can serve multiple variants of the page without needing to rely on HTTP caches such as Varnish; we cache each module on the page in Redis and construct the page using the cached fragments instead.

When I was working on Node.js in Practice, the development team at the publisher kept pushing us to prove why Node is fast.  They were concerned that it was all hyperbole, so we were constantly challenged to argue our performance assertions.  I was encouraged to read that the programmers at the BBC have found Node to perform well enough for their large scale site, so if this project goes well it'll be a great testimonial for Node.

Andrew also mentions that they've used React and Browserify.  I've increasingly found Browserify to be the right choice for front-end work:

> On the front end we have embraced new technologies such as isomorphic Javascript using ReactJS. This allows us to execute our Javascript templates on both the server and the client meaning that users without Javascript can still load a basic version of the page. The technology will also allow us to quickly develop modules that can periodically update themselves with live data from around the BBC. All our scripts are bundled together using Browserify, which allows us to mix both the AMD and the CommonJS module loading systems. Utilising a mix of these two loading systems means we are not restricted in our choice of open source libraries because of the mechanism implemented in a particular module.

The post has some good comments, so it's worth at least reading through the top ones.  One by "Twirrim" suggests that the site could be further optimised to reduce the amount of separate JavaScript files:

> In the US, 3G & 4G typically see 90-100ms latency per request. Mobile Yslow is reporting that you've got 21 javascript scripts on the page. IIRC The android browser will limit itself to 4 threads retrieving content typically so that's (21/4 * 100ms) 525ms just lost in latency requesting the javascript, let alone actually downloading it and the overhead of the javascript renderer.

For those of us who are investing in React, Browserify, and Node, this article is encouraging and interesting.  And if you've got your own successful server-side JavaScript stories that you'd like to share, why not [get in touch](http://contact.dailyjs.com)?
