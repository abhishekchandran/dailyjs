---
layout: post
title: "Node Roundup: 0.11.5, nvi, signobj"
author: "Alex Young"
categories: 
- node
- modules
- vim
- security
- crypto
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a>.
</div>

###Node 0.11.5

[Node 0.11.5 was released this week](http://blog.nodejs.org/2013/08/06/node-v0-11-5-unstable/).  This unstable version updates v8 and uv.  It also includes fixes for buffer, child_process, dgram, fs, https, openssl, os, tls, and util.

[The patch for fs by Trevor Norris is interesting](https://github.com/joyent/node/pull/5747/files#r5360078) ([pull request](https://github.com/joyent/node/pull/5747)) -- rather than writing strings to a buffer and then the disk, it changes `fs.js` and `src/node_file.cc` to write directly to the disk instead.

###nvi

nvi (GitHub: [mikesmullin / nvi](https://github.com/mikesmullin/nvi), License: _GPLv3_, npm: [nvi](https://npmjs.org/package/nvi)) by Mike Smullin is a 'very opinionated Vi clone'.  I tried installing it with `npm install -g nvi`, but it wouldn't run; I had to check out the repository manually.  It doesn't clone Vi or Vim in a way that I think it's fair to call 'clone' -- I can't seem to get `hjkl` to move the cursor, and the modes have been changed to include 'COMBO' mode instead of Normal mode which makes using it extremely confusing for a seasoned Vim veteran.

Despite all that, and the fact that [the name nvi is a bad choice](http://en.wikipedia.org/wiki/Nvi), I find the project interesting because making complex text user interfaces isn't an easy task.  Also, Mike's nvi is focused on collaborative features, which potentially makes Node a great fit.

###signobj

Django has a [cryptographic API](https://docs.djangoproject.com/en/dev/topics/signing/) for setting and reading signed cookies, and presumably you can also use this to sign API responses for RESTful JSON APIs.  Inspired by this, signobj (GitHub: [Submersible / node-signobj](https://github.com/Submersible/node-signobj), License: _MIT_, npm: [signobj](https://npmjs.org/package/signobj) by Ryan Munro allows you to sign JSON data with a SHA-1 HMAC:

> `signobj()` - Signs data with secret, you can also pass in some extra hidden data that is used when hashing. This can be useful if you're creating an access token, and you want it to become invalid when they change their password, and also don't want the password with the public data.

Ryan said he's been using it to sign cookies and localStorage sessions.
