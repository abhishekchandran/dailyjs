---
layout: post
title: "Web Servers in Firefox OS, Marionette Inspector"
author: Alex Young
categories:
- firefox
- tools
- frameworks
- articles
- backbone
---

### Embedding an HTTP Web Server in Firefox OS

Justin D'Arcangelo sent in a detailed article about web servers in Firefox OS: [Embedding an HTTP Web Server in Firefox OS](https://hacks.mozilla.org/2015/02/embedding-an-http-web-server-in-firefox-os/).

> ... we've been looking at harnessing technologies to collectively enable offline P2P connections such as Bluetooth, NFC and WiFi Direct.
>
> By utilizing HTTP, we would already have everything we'd need for apps to send and receive data on the client side, but we would still need a web server running in the browser to enable offline P2P communications. While this type of HTTP server functionality might be best suited as part of a standardized WebAPI to be baked into Gecko, we actually already have everything we need in Firefox OS to implement this in JavaScript today!

The article uses [justindarc/fxos-web-server](https://github.com/justindarc/fxos-web-server) which is a JavaScript web server built with [TCPSocket](https://developer.mozilla.org/en-US/docs/Web/API/TCPSocket), a raw TCP socket API in JavaScript.

> The possible use cases enabled by embedding a web server into Firefox OS apps are nearly limitless. Not only can you serve up web content from your device to a desktop browser, as we just did here, but you can also serve up content from one device to another. That also means that you can use HTTP to send and receive data between apps on the same device! Since its inception, FxOS Web Server has been used as a foundation for several exciting experiments at Mozilla.

So it seems like Firefox OS is getting the kind of advanced features that we've seen appear (and in some cases disappear) in Chrome OS, where you get access to native APIs to create desktop-like experiences.

###Marionette Inspector

Jason Laster wrote to me about the [Marionette](http://marionettejs.com/) Chrome Extension, known as the Marionette Inspector.  There's a [video about it](https://www.youtube.com/watch?v=jbGm3mJXh_s&feature=youtu.be), and you can download it from the [Chrome web store](https://chrome.google.com/webstore/detail/marionette-inspector/fbgfjlockdhidoaempmjcddibjklhpka).

It has some features that are pretty unique, like visualisations for the view hierarchy with the UI tree, and more friendly handling for inspecting Backbone models and events.  Rather than seeing a complex JavaScript object, you'll see properties grouped under UI, Events, Model, and Properties.

It makes building apps with Marionette more like using the tools you might expect from an IDE, so you should try it out if you already use Marionette or are a Backbone fan that hasn't yet tried it.
