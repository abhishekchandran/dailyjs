---
layout: post
title: "Backbone and Azure, Yass.js, grunt-stripmq"
author: "Alex Young"
categories: 
- backbone.js
- mobile
- css
- grunt
---

###Backbone Adapter for Azure

Olivier Bloch sent in a [Backbone adapter for Windows Azure](http://aka.ms/BackboneAdapterForWAMS) (GitHub: [MSOpenTech / backbone-azure-mobile-services](https://github.com/MSOpenTech/backbone-azure-mobile-services), License: _Apache 2.0_).  It's distributed by Microsoft Open Technologies, and syncs data with the [Windows Azure Mobile Data Service](http://www.windowsazure.com/en-us/develop/mobile/tutorials/get-started-with-data-dotnet/).

If you're interested in trying out the server-side API without Backbone.js, I noticed there's a tutorial here: [Get started with data in Mobile Services](http://www.windowsazure.com/en-us/develop/mobile/tutorials/get-started-with-data-js/).

To use Azure with Backbone, all you need to do is include the adapter, an [additional JavaScript file provided by Microsoft](http://www.windowsazure.com/en-us/develop/mobile/tutorials/get-started-html/), and some settings for your collections:

{% highlight javascript %}
var People = Backbone.Collection.extend({
  client: client,
  table: 'Table1',
  model: Person
});
{% endhighlight %}

The authors have included build scripts (Grunt) and tests (Jasmine).

###Yass.js

[Yass.js](http://eightmedia.github.io/yass.js/) (GitHub: [EightMedia / yass.js](https://github.com/EightMedia/yass.js), License: _MIT_) by Jorik Tangelder is an adaptive image script that adds support for [srcset](http://www.w3.org/html/wg/drafts/srcset/w3c-srcset/) tailored to mobile browsers.  Once `yass.js` has been added after the last image on a page, it will ensure the optimum image is loaded.

It's currently very small (less than 500 bytes when compressed), and has been tested in Chrome 28, Android 4.2, IOS6, BlackBerry10 and IE6.

###grunt-stripmq

grunt-stripmq (GitHub: [jtangelder / grunt-stripmq](https://github.com/jtangelder/grunt-stripmq), License: _MIT_, npm: [grunt-stripmq](https://npmjs.org/package/grunt-stripmq)) also by Jorik Tangelder is a "mobile-first CSS fallback":

> A Grunt task to generate a fallback version of your fancy mobile first stylesheet. Since IE9 doesn't support media queries, you can use a JavaScript like respond.js to enable this, or generate a fallback version with this task.

So if you've invested a lot of time developing modern, mobile-optimised sites, then you should be able to jam them through Grunt to spit out something desktop-friendly.
