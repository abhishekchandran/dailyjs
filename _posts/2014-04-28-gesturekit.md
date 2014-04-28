---
layout: post
title: "GestureKit"
author: "Alex Young"
categories:
- mobile
- libraries
---

![GestureKit](/images/posts/gesturekit.png)

[GestureKit](http://www.gesturekit.com/) (GitHub: [RoamTouch / gesturekit.js](https://github.com/RoamTouch/gesturekit.js), License: _Apache 2.0_) by Guille Paz and RoamTouch is an SDK for creating and recognising gestures in mobile interfaces.  There's an open source client-side library that has an event-based API for responding to gestures.

Gestures can be recorded on a mobile device and then used on different platforms.  The project's homepage has examples for Android, iOS, and JavaScript.

GestureKit is backed by a service for storing metrics on gestures.  Applications can work offline though, the underlying data is cached on startup.

Right now it seems like the server part of the project is closed source, but the [FAQ](http://learn.gesturekit.com/faq) states that part of the API will be opened, and they're looking for contributors:

> GestureKit has a Github repos for community pushes that you will be able to contribute. We are planning to open a part of the API, specially the actions performed with the gestures and a plugin interface to integrate new stuff to the service.

The thing I like about this project is the idea that you can draw shapes to trigger specific functionality.  The example is a music app that uses two arrows to mean skip forward or back.
