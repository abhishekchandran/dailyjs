---
layout: post
title: "Node Roundup: Node 0.8.27 and 0.10.29, BipIO, Reducto"
author: "Alex Young"
categories:
- node
- modules
- npm
---

###Node 0.8.27 and 0.10.29

You may be surprised to see a Node 0.8 release here, but [0.8.27 and 0.10.29 have been updated](http://blog.nodejs.org/2014/06/16/openssl-and-breaking-utf-8-change/) to fix an OpenSSL and UTF-8 encoding issue:

> Additionally these releases address the fact that V8 UTF-8 encoding would allow unmatched surrogate pairs. That is to say, previously you could construct a valid JavaScript string (which are stored internally as UCS-2), pass it to a Buffer as UTF-8, send and consume that string in another process and it would fail to interpret because the UTF-8 string was invalid.
>
> This breaks backward compatibility for the specific reason that unsanitized strings sent as a text payload for an RFC compliant WebSocket implementation should result in the disconnection of the client. If the client attempts to reconnect and receives another invalid payload it must disconnect again. If there is no logic to handle the reconnection attempts, this may lead to a denial of service attack.

The post includes an example with `Buffer`, and demonstrates how even if you're not explicitly creating `Buffer` instances from strings Node might still do it behind the scenes.

###BipIO

[BipIO](https://bip.io/) (GitHub: [bipio-server / bipio](https://github.com/bipio-server/bipio), License: _GPLv3_) an API platform for consuming and composing APIs based on graph definitions and pipelines.  You can run your own server, and there's a closed source web UI that you can [sign up to](https://bip.io/signup):

> If you're familiar with Yahoo Pipes, IFTTT, Zapier, Mulesoft, Cloudwork or Temboo - the concept is a little similar. The server has a small footprint which lets you create and automate an internet of things that matter to you. It can be installed alongside your existing open source app or prototype for out-of-band message transformation, feed aggregation, queuing, social network fanout or whatever you like, even on your Rasberry Pi.

It uses MongoDB and RabbitMQ, and the readme has help for setting it up on a server with Monit.

###Reducto

Reducto (GitHub: [michaelleeallen / reducto](https://github.com/michaelleeallen/reducto), License: _MIT_, npm: [reducto](https://www.npmjs.org/package/reducto)) by Michael Allen is configuration framework for Express that aims to simplify the creation of routes for APIs.

> The main goal of reducto is to break apart the routing mechanism into smaller, more cohesive components. By reducing your app to just middleware, data transforms, and reusable service calls you end up with a smaller set of code to reason about and thus make your app easier to write and maintain.

You can create routes using JSON files that map middleware, service handlers, data fixtures, and transform functions to routes.  It also supports services, which are callable HTTP endpoints.  It comes with an example application that shows weather for a given zip code.
