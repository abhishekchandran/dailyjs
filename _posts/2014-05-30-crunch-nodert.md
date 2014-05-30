---
layout: post
title: "Crunch, NodeRT"
author: Alex Young
categories:
- node
- mathematics
---

###Crunch

[Crunch](http://crunch.secureroom.net/) (GitHub: [vukicevic / crunch](https://github.com/vukicevic/crunch), License: _MIT_) by Nenad Vukicevic is an arbitrary-precision integer arithmetic library, with a focus on speed.  It has no dependencies, and the project includes examples for finding prime-numbers, generating keys for RSA, encryption, and decryption.

The examples also demonstrate using WebWorkers with the library, so you could farm out mathematical operations to multiple workers.  Crunch includes unit tests and documentation in the readme file.

###NodeRT

[NodeRT](https://github.com/NodeRT/NodeRT) is a WinRT module generator for Node:

> NodeRT automatically exposes Microsoft's WinRT APIs to Node.js by generating Node modules. This enables Node developers to write code that consumes native Windows capabilities. The generated APIs are (almost) the same as the WinRT APIs listed in MSDN.

This is an example of [windows.devices.geolocation](http://msdn.microsoft.com/library/windows/apps/br225603):

{% highlight javascript %}
var geolocation = require('windows.devices.geolocation');
var locator = new geolocation.Geolocator();

locator.getGeopositionAsync(function(err, res) {
  if (err) {
    console.error(err);
    return;
  }

  console.info('(', res.coordinate.longitude, ',',  res.coordinate.latitude, ')');
});
{% endhighlight %}

The project has fairly detailed documentation in the readme, including the [requirements](https://github.com/NodeRT/NodeRT#Prerequisites) which includes VisualStudio 2013.
