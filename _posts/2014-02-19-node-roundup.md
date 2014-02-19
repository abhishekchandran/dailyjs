---
layout: post
title: "Node Roundup: 0.10.26, DozerJS, Keybase"
author: Alex Young
categories:
- node
- modules
---

###Node 0.10.26

[Node 0.10.26](http://blog.nodejs.org/2014/02/18/node-v0-10-26-stable/) is out.  It includes updates for V8, npm, and uv, and fixes for several core modules, including crypto, fs, and net.

###DozerJS

![DozerJS](/images/posts/dozerjs.png)

[DozerJS](http://dozerjs.com/) (GitHub: [DozerJS / dozerjs](https://github.com/DozerJS/dozerjs), License: _MIT_, npm: [dozerjs](https://npmjs.org/package/dozerjs)) is an Express-based project that aims to make it easier to develop MVC-style REST-based applications.

It looks like the focus is on simplifying the server-side implementation so you can focus on the UI.  The conventions used for the server-side structure seem to follow the popular wisdom: route separation, simple models with validation, and HTTP verbs for CRUD operations.

###Keybase

![Keybase](/images/posts/keybase.png)

[Keybase](https://keybase.io/) (GitHub: [keybase / node-installer](https://github.com/keybase/node-installer)) is a public key sharing tool that you can install with npm: `npm install -g keybase-installer`.  It allows you to associate several keys with a single identity:

>  In one command, Keybase has acquired maria's public key, her keybase username, and her public identities, and confirmed they're all her, using GnuPG to review a signed tweet and gist she posted.

I think it's an extremely interesting project -- the website is clear, and I like the idea of being able to confirm identities for collaborating with people online.  Using npm to distribute the client seems like a smart approach.
