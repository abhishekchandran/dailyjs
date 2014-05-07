---
layout: post
title: "Node Roundup: 0.10.28, 0.11.13, CSRF Vulnerability in Express, Generators in Node, Wolfpack"
author: "Alex Young"
categories:
- node
- modules
- npm
- generators
- testing
---

###Node 0.10.28, 0.11.13

Node has been updated to [0.10.28](http://blog.nodejs.org/2014/05/02/node-v0-10-28-stable/) and [0.11.13](http://blog.nodejs.org/2014/05/02/node-v0-11-13-unstable/).

Version 0.10.28 was a quick update to the earlier [0.10.27](http://blog.nodejs.org/2014/05/01/node-v0-10-27-stable/) release, which updates C++ dependencies (openssl, libuv) as well as several core modules.  One important change was the update of openssl to 1.0.1g.

###CSRF Vulnerability in Express

Connect and Express have a vulnerability in the CSRF middleware component that means you can bypass it by making a `GET` request with a method override parameter:

> Connect's methodOverride middleware allows an HTTP request to override the HTTP verb with the value of the _method post parameter or with the x-http-method-override header. As the declaration order of middlewares determines the execution stack in Connect, it is possible to abuse this functionality in order to bypass the standard Connect's anti-CSRF protection.

> Connect's CSRF middleware does not check CSRF tokens in case of idempotent verbs (GET/HEAD/OPTIONS, see csurf/index.js). As a result, it is possible to bypass the security control by sending a GET request with a POST MethodOverride header or parameter.

Read more at [NibbleSecurity](http://blog.nibblesec.org/2014/05/nodejs-connect-csrf-bypass-abusing.html).

###Generators in Node

[Generators in Node.js: Common Misconceptions and Three Good Use Cases](http://strongloop.com/strongblog/how-to-generators-node-js-yield-use-cases/) is a post by Marc Harter that explains how generators work from a Node developer's perspective.

> Generators are function executions that can be suspended and resumed at a later point; a lightweight coroutine. This behavior happens using special generator functions (noted by `function*` syntax) and a couple of new keywords (`yield` and `yield*`) which are only used in the context of a generator

###Wolfpack

Wolfpack (GitHub: [fdvj / wolfpack](https://github.com/fdvj/wolfpack), License: _MIT_, npm: [wolfpack](https://www.npmjs.org/package/wolfpack)) by Fernando De Vega is a [SailsJS](http://sailsjs.org/#!) model testing library that uses SinonJS to mock the database and spy on models.  That means you don't need a real database to run unit tests.

> If you have Backbone testing backgrounds, this will be familiar to you. When testing a backbone model or collection, you instantiate it and provide mock data to test the methods. Rarely do you need your model or collection to communicate with the server to provide the results. That's because you want to test your model or collection, not how or if backbone is doing what it is supposed to do.
