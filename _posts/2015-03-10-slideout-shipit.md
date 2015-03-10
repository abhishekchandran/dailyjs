---
layout: post
title: "Slideout.js, Shipit vs Flightplan"
author: Alex Young
image: "/images/posts/slideout.gif"
categories:
- deployment
- articles
- ui
- libraries
---

###Slideout.js

[Slideout.js](http://mango.github.io/slideout/) (GitHub: [mango/slideout](https://github.com/mango/slideout), License: _MIT_, npm: [slideout](https://www.npmjs.com/package/slideout)) by Guille Paz is a touch-based slideout navigation menu for mobile applications.  It doesn't use any dependencies, and the markup is sensible.  It has CSS transforms and transitions, and uses native scrolling.

The markup is based on HTML5 tags, so you can define the navigation panel with a `nav` element.  It works in most browsers, and the base version of IE is 10.

The JavaScript API uses a `Slideout` constructor function, and it accepts options for animations, duration, and the necessary DOM elements.

One nice thing about this library is there are lots of ways to install it: npm, spm, bower, and component are all supported.

###Shipit vs Flightplan

I've written about Shipit and Flightplan, but I haven't yet used both deployment solutions for anything serious.  John Munsch has written a long post about his experiences [using both Shipit and Flightplan](http://johnmunsch.com/2015/03/08/shipit-vs-flightplan-for-automated-administration/) with a DigitalOcean server:

> I did everything from start to finish myself and I felt duly proud about having built something from scratch and launched it no matter how small it was.
> The tasks covered by my scripts were: initial machine configuration, updating of Ubuntu (mainly to get security fixes), deployment, and creating a SSH shell to the remote server.

Using a cheap VM can be very affordable if you want to host your own email, web services, and maybe use it for IRC.  Deployment is naturally more work than something like Heroku, but Shipit and Flightplan can really streamline things.

John's article compares the pros and cons of each library, and he's included the scripts he used for deployment.
