---
layout: post
title: "Socket.IO Debugging"
author: Alex Young
categories:
- npm
- node
- websockets
---

How do you debug WebSockets, other than inserting `console.log` all over the place?  One technique is to look at the Frames tab, under Network, in WebKit Inspector.

<div class="image">
  <img src="/images/posts/websocket-debugging-frames.png" alt="" />
  <small>The Frames tab in WebKit Inspector.</small>
</div>

The term "frames" refers to the data that is sent in a WebSocket connection.  Unfortunately, I've been doing some work with WebSockets inside a desktop application, so I can't easily see WebKit inspector.

Diego Costantino sent in ThreePin (GitHub: [dieguitoweb / ThreePin](https://github.com/dieguitoweb/ThreePin), License: _MIT_, npm: [threepin](https://npmjs.org/package/threepin), bower: _dieguitoweb/ThreePin_), a tool for developing and testing software that uses Socket.IO and Node:

> ThreePinJS is a stress-free test environment for Socket.IO allows you to test your WebSocket server code before you write the client code.

It uses a configuration file called `threepin.json` that sets up a server, and a list of events to listen for and send.  The readme has a full example.

Once the server is configured, you can use any local HTTP server you want to serve a simple HTML file that connects and runs through the event list.  It means you can focus on the server-side logic before worrying about the client-side code.

I'm still looking for options to help test and debug Socket.IO projects, but I thought ThreePin was an interesting stab at the problem.
