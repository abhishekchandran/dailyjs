---
layout: post
title: "Echotube, Community Updates"
AUthor: Alex Young
categories:
- media
- google
- community
- backbone.js
---

###Echotube

![Echotube](/images/posts/echotube.png)

[Echotube](http://echotu.be/#play/video/cvz9uSK3zXo) (GitHub: [orizens / echoes](https://github.com/orizens/echoes), License: _MIT_) by Oren Farhi is a Backbone.js and RequireJS YouTube media manager.  It's open source, and the code is all JavaScript, so you can easily see how the author has structured the Backbone code around YouTube's API.

The design is derived from Bootstrap, but there are a lot of custom widgets and CSS transitions which keep it feeling original.  Also, Jasmine tests have been included, which is interesting because it seems like a [slightly awkward thing to test](https://github.com/orizens/echoes/blob/master/test/src/YoutubeResponse.js).

If you're looking for fully-fleshed out Backbone/RequireJS applications to learn from then give it a look.

###Community Updates

I occasionally receive messages about major updates to libraries and products that I don't always write about, but I thought it would be nice to start publishing those as well.  If you read about BromBone -- a service that provided access to headless browsers -- then you might be interested to hear that [BromBone is now a service for bringing better SEO to single page apps](http://www.brombone.com/).  It works by adding redirects to `yoursite.brombone.com` based on the crawler's user agent.  The documentation has a simple `.htaccess` file which will work for Apache.

Also of note is Vincent Voyer's [lazyload](https://github.com/vvo/lazyload) script has been updated to 2.0:

* Support added for [retina/hd images](https://github.com/vvo/lazyload#hidpi-images)
* Lazyload iframes
* [Lazyload widgets](http://vvo.github.io/lazyload/)
* Mocha tests
* Available through bower under `lazyload`

Feel free to contact us about your module/script/app's major updates and I shall endeavour to find space to write about it.
