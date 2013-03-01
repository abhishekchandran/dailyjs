---
layout: post
title: "localStorage DOS, Lunr.js, Vlug"
author: "Alex Young"
categories: 
- security
- libraries
- search
- benchmarking
- node
---

###localStorage DOS

Even though the [Web Storage](http://www.w3.org/TR/webstorage/) specification says user agents should limit the amount of space used to store data, [a new exploit uses it to store gigabytes of junk](http://arstechnica.com/security/2013/02/exploit-lets-websites-bombard-visitors-pcs-with-gigabytes-of-data/).  The exploit is based around storing data per-subdomain, which gets around the limits most browsers have already implemented.  Users testing it found Chrome would crash when run in incognito mode, but Firefox was immune to the attack.

Other security researchers have raised concerns about `localStorage` in the past.  [Joey Tyson talked about storing malicious code in localStorage](http://securitymusings.com/article/3159/how-a-platform-using-html5-can-affect-the-security-of-your-website), and Todd Anglin wrote about some of the more [obscure facts about localStorage](http://htmlui.com/blog/2011-08-23-5-obscure-facts-about-html5-localstorage.html) which touches on security.

###Lunr.js

Oliver Nightingale from New Bamboo sent in his extremely well-presented [full-text browser-based search library](http://blog.new-bamboo.co.uk/2013/02/26/full-text-search-in-your-browser) (GitHub: [olivernn / lunr.js](https://github.com/olivernn/lunr.js), License: _MIT_), which indexes JSON documents using some of the core techniques of larger server-side full-text search engines: tokenising, stemming, and stop word removal.

> By removing the need of extra server side processes, search can be a feature on sites or apps that otherwise would not have warranted the extra complexity.

[Trie](http://en.wikipedia.org/wiki/Trie) is used for mapping tokens to matching documents, so if you're interested in JavaScript implementations of data structures then take a look at the source.  The source includes tests and benchmarks, and a build script so you can generate your own builds.

###Vlug

[Vlug](http://pllee.github.com/vlug/docs/) (GitHub: [pllee / vlug](https://github.com/pllee/vlug), License: _MIT_, npm: [vlug](https://npmjs.org/package/vlug)) by Patrick Lee is a small instrumentation library for benchmarking code without manually adding log statements.  The `Vlug.Interceptor` object takes a specification of things to log, which will dynamically invoke calls to `console.time` and `console.timeEnd` to collect benchmarks.

Patrick has tested it with browsers and Node, and has included `Vlug.Runner` for running iterations on functions.  The readme and homepage both have documentation and examples.
