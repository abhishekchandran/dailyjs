---
layout: post
title: "Node Roundup: 0.11.10, Ducky, Test-driving a Node.JS API"
author: Alex Young
categories:
- node
- modules
- testing
- types
---

###Node 0.11.10

[Node 0.11 is now pushing double figures](http://blog.nodejs.org/2013/12/31/node-v0-11-10-unstable/).  The three main dependencies have been updated (http_parser, uv, v8), and the core modules have a lot of fixes.

###Ducky

[Ducky](http://duckyjs.com/) (GitHub: [rse / ducky](https://github.com/rse/ducky), License: _MIT_, npm: [ducky](https://npmjs.org/package/ducky)) by Ralf S. Engelschall is a library for querying and validating objects.

The `ducky.select` method accepts an object and a "path" -- this path is based on dot notation.  The `ducky.validate` method accepts an object and a string representation of its types.  The validation syntax is based on JSON with some regular expression hints.

Ralf has included tests based on [Chai](https://npmjs.org/package/chai), and you can also use this module in client-side projects.

###Test-driving a Node.JS API

[Test-driving a Node.JS API](http://www.jorisooms.be/testing-your-node-api-with-supertest/) by Joris Ooms is a blog post about setting up a test-driven project based on Express, SuperTest, and Mocha.

At the end he says:

> Often, routes are locked behind authentication (with, for example, PassportJS). We can test these just as easily with supertest, through its lower-level module superagent. I will cover this in a future blog post.

I think he's going to talk about the technique I use for testing my web applications, where authentication is handled with [SuperAgent](https://github.com/visionmedia/superagent) and cookies.  It's a bit awkward to set up, so it'll be interesting to see what he says.
