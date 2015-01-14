---
layout: post
title: "Node Roundup: io.js 1.0.1, jsop, HAP-NodeJS"
author: Alex Young
image: "/images/posts/nodehomekit.png"
categories:
- node
- modules
- libraries
- forks
---

###io.js 1.0.1

io.js has now released version [1.0.0 and 1.0.1](https://iojs.org/?1.0.0).  There's a [changelog with a summary](https://github.com/iojs/io.js/blob/v1.x/CHANGELOG.md) that explains what's changed from Node 0.10.35 to 1.0.0.  Things are slightly more complicated by the fact that changes from Node's unstable branch are merged in as well:

> The io.js codebase inherits the majority of the changes found in the v0.11 branch of the joyent/node repository and therefore can be seen as an extension to v0.11.

There are some important ES6 changes in io.js, partly because V8 has been updated, but also because you don't need to use the [--harmony flag](https://iojs.org/es6.html) for many useful ES6 features:

> All harmony features are now logically split into three groups for shipping, staged and in progress features:
> All shipping features, the ones that V8 has considered stable, like generators, templates, new string methods and many others are turned on by default on io.js and do NOT require any kind of runtime flag.

The other binary libraries (C-Ares, `http_parser`, libuv, npm, openssl, punycode) and Node's core modules have also been updated.  There are even some new core modules: see [smalloc](https://iojs.org/api/smalloc.html) and [v8](https://iojs.org/api/v8.html).  The smalloc module can be found in Node 0.11.x, but [v8 was reintroduced by Ben Noordhuis](https://github.com/iojs/io.js/commit/db595b2de6933bfda5a1371fc84d14bc9b8a37dd) to io.js:

> I introduced this module over a year ago in a pull request as the v8 module but it was quickly subsumed by the tracing module.
>
> The tracing module was recently removed again and that is why this commit introduces the v8 module again, including the new features it picked up commits d23ac0e and f8076c4.

I realise that the existence of io.js is confusing and potentially worrying for Node developers.  If this is new to you, take a look at the [io.js Project Governance](https://github.com/iojs/io.js/blob/v1.x/GOVERNANCE.md#readme) and [this comment by duncanawoods on Hacker News](https://news.ycombinator.com/item?id=8884874):

> In their words, io.js is "A spork of Node.js with an open governance model".
>
> Sporking: Creating a fork that you would really like to become the next main-line version but you kinda have to prove its awesome first (sporks are pretty awesome)

###jsop

With the release of io.js 1.0.0 (and Node 0.11.13), typicode has created jsop (GitHub: [typicode/jsop](https://github.com/typicode/jsop), License: _MIT_, npm: [jsop](https://www.npmjs.com/package/jsop)), a one-way data binding for JSON files.  It's built with `Object.observe`, and allows you to watch a file like this:

{% highlight javascript %}
var jsop = require('jsop')

var config = jsop('config.json')
config.foo = 'bar'
{% endhighlight %}

This will actually write the change to the JSON file.  There's a before and after example in the readme, so you can see how much syntax this module saves.  This module is based on [observed](https://www.npmjs.com/package/observed), which provides `Object.observe` with nested object support.

The same author also sent in [homerun](https://github.com/typicode/homerun), which is a module that takes advantage of npm 2's support for script arguments.  This project basically allows you to get a command-line interface for free, once you've run `npm link` or `npm publish`.

###HAP-NodeJS

[Node and HomeKit](/images/posts/nodehomekit.png)

Other than watches, the smartphone/tablet vendors are trying to push the idea of the connected home.  I was looking into ways to script my Wi-Fi lightbulbs and ran into [HAP-NodeJS](https://github.com/KhaosT/HAP-NodeJS):

> HAP-NodeJS is a Node.js implementation of HomeKit Accessory Server.
> With this project, you should be able to create your own HomeKit Accessory on Raspberry Pi, Intel Edison or any other platform that can run Node.js :)
> The implementation may not 100% follow the HAP MFi Specification since MFi program doesn't allow individual developer to join.

[HomeKit](https://developer.apple.com/homekit/) is Apple's iOS 8 framework for controlling electronics in the home.  The author notes that the project isn't necessarily 100% compatible with the [HAP MFi specification](https://mfi.apple.com/MFiWeb/getFAQ.action), but there's a [short video of it working](http://instagram.com/p/t4cPlcDksQ/) with an iPhone.  That means you should be able to get an iOS device to connect to anything that is capable of running the HAP-NodeJS server.

