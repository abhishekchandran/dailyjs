---
layout: post
title: "Node Roundup: Money and npm, Isaac Schlueter Interview, KOAN"
author: "Alex Young"
categories:
- node
- modules
- realtime
- npm
---

###Nebulous Profit Meditations

Isaac Schlueter wrote a long article on the npm blog about [how npm Inc. will make money](http://blog.npmjs.org/post/80997676347/nebulous-profit-meditations).  It has some hints about the future of advertising on npm:

> In my opinion, a good example of advertising done very well is the hosting page on WordPress.org. The services offered are beneficial to WordPress users, and are offered in such a way as to avoid distracting from the core product. The focused curation increases the value, and provides a strong incentive for the advertised products to maintain their quality or risk losing their position.
> We will be pursuing similarly focused and curated advertising partnerships on the npm website, in ways that benefit our users as well as our technology partners.

And GitHub's influence:

> When I describe our plans to people, they often nod and say, "Oh, the GitHub model, ok." I'm sure that "public for free, private costs money" isn't new with GitHub. However, pursuing that kind of model, while at the same time acknowledging that coding is a social activity, really was a master stroke in the history of software development. I'm very thankful that they've helped pave the way for people to recognize this pattern.

###Meet the Face Behind npm

The Modulus hosting company blog has an [interview with Isaac](http://blog.modulus.io/isaac-interview), with some history prior to Node and npm:

> At Yahoo!, I grew increasingly frustrated that I had to switch back and forth between PHP and JavaScript, and Google had just open sourced their V8 engine, so I started trying to seriously get into doing JavaScript on the server. I got involved with the K7 project, and started studying web servers in more detail. There was also SpiderApe, and v8cgi, and a bunch of other projects. Narwhal caught my eye, and I spent a bunch of time messing with that.

I seem to remember making IRC bots with Rhino and Java sockets, then Node came along and changed everything!

###KOAN

[KOAN](http://www.koanjs.com/login.html) (GitHub: [soygul / koan](https://github.com/soygul/koan)) by Teoman Soygul is a full stack boilerplate that uses Koa, AngularJS, Node, and MongoDB.  Unlike other similar projects, this one has WebSocket features baked in.

A KOAN app uses JSON-RPC for syncing data with the server, and the readme has details on how to deploy this to Heroku (using `labs:enable websockets`).
