---
layout: post
title: "Node Roundup: 0.10.33, Node.js Best Practices, Puer"
author: "Alex Young"
image: "/images/posts/keybase-node-cli.png"
categories:
- modules
- libraries
- security
- live-reload
---

###0.10.33 and Signing Validation

[0.10.33](http://blog.nodejs.org/2014/10/23/node-v0-10-33-stable/) came out last week, which fixes the POODLE vulnerability by disabling SSLv2/SSLv3.  You may find this release breaks legacy browsers like IE6:

> If you wish to enable SSLv2 or SSLv3, run node with the `--enable-ssl2` or `--enable-ssl3` flag respectively. In future versions of Node.js SSLv2 and SSLv3 will not be compiled in by default.

If you see errors like "wrong version number" when connecting to other servers, then you may want to upgrade those as well:

> If your application is behaving as a secure client and communicating with a server that doesn't support methods more secure than SSLv3 then your connection won't be able to negotiate and will fail. In this case your client will emit an `error` event. The error message will include `'wrong version number'`.

On the topic of security, when I was reading the release notes I realised that they're signed by the author's PGP signature.  If you ever want to validate these signatures then you can do so with [Keybase](http://keybase.io/).  Keybase has a nice command-line tool that you can install with `npm install keybase`.  After signing in, you can verify the message:

![Node release notes verification](/images/posts/keybase-node-cli.png)

In the screenshot you should be able to see that the message was written by tjfontaine.  Keybase has a web interface as well, so you can just paste in the signature:

![Web verification](/images/posts/keybasenode.png)

###Node.js Best Practices

Alan James sent in an interesting and useful resource called [Node.js Best Practices](http://justbuildsomething.com/node-js-best-practices/) (GitHub: [alanjames1987 / Node.js-Best-Practices](https://github.com/alanjames1987/Node.js-Best-Practices)).  It lists some things that the author has found useful when teaching Node to beginners, like checking for errors in callbacks, `use strict`, and avoiding requiring modules inside functions.

One of the tips is to save a reference to `this`.  Teaching JavaScript's scope rules is indeed problematic, and although I often find `.bind` cleaner that is an additional piece of cognitive baggage that is hard to explain to beginners.  Alan is open to pull requests for the document on GitHub, so it may be worth helping to expand some sections like this one.

###Puer

[Puer](https://github.com/leeluolee/puer) (npm: [puer](https://www.npmjs.org/package/puer)) is a static server for client-side development that can automatically update CSS without a page reload.  It supports Connect middleware, and can mock requests.

I still use solutions that force me to reload the content in the browser, usually based on Grunt or Gulp modules.  These can have a small delay that forces me to reload twice in some cases, so I'm always trying out modules like this to find a better one.
