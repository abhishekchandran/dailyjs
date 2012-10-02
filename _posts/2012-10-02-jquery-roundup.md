---
layout: post
title: "jQuery Roundup: jQuery UI 1.8.24, HTML5 Google Authenticator, pXY.js"
author: Alex Young
categories:
- jquery
- jquery-ui
- plugins
- Canvas
- security
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###jQuery UI 1.8.24

[jQuery UI 1.8.24](http://blog.jqueryui.com/2012/09/jquery-ui-1-8-24/) is out, which is a maintenance release:

> This update brings bug fixes for Datepicker, Draggable, Droppable and Sortable, as well as adding support for jQuery 1.8.2. This is likely to be the last release in the 1.8 family; you can expect 1.9.0 very soon. For the full list of changes, see the changelog.

The jQuery UI 1.9 release candidates have been around for a while now.  Check out the [1.9 RC tags](https://github.com/jquery/jquery-ui/tree/1.9.0-rc.1) on GitHub for more.

###HTML5 Google Authenticator

I use [Google Authenticator](http://support.google.com/a/bin/answer.py?hl=en&hlrm=en&answer=1037451), which is a two-step verification implementation.  Google have released corresponding mobile apps which support multiple credentials.  This means third-party services can plug into Google Authenticator, so users only need one app to manage all of their credentials.  This works because Google Authenticator is built on open standards, and uses the [Time-based One-time Password algorithm](http://tools.ietf.org/id/draft-mraihi-totp-timebased-06.html).

The TOPT algorithm has already been implemented in [JavaScript back in 2011 by Russ Sayers](http://blog.tinisles.com/2011/10/google-authenticator-one-time-password-algorithm-in-javascript/):

> Turns out the algorithm used to generate the OTPs is an open standard. When you set-up an account in the smartphone app you are storing a key that's used to create a HMAC of the current time.

This has now been ported to a polished [HTML5 Google Authenticator](https://github.com/gbraad/html5-google-authenticator) project, built with jQuery Mobile by Gerard Braad.  He's also deployed a demo version at [gauth.apps.gbraad.nl](http://gauth.apps.gbraad.nl/).

Cryptography and security in client-side code will always be a tricky subject, but hopefully this kind of project will help demystify two-factor authentication and encourage more web application authors to offer it to those of us who are interested in it.

###pXY.js

[pXY.js](http://o-0.me/pXY/) (GitHub: [leeoniya / pXY.js](https://github.com/leeoniya/pXY.js), License: _MIT_) by Leon Sorokin is an API for analysing the pixels in a `Canvas` elements.  The author suggests using it as an algorithm visualisation tool for problems relating to OCR segmentation and document feature extraction.

The documentation has runnable examples of the major API features.  For example, the [Scanning pXY documentation](http://o-0.me/pXY/#scanning) shows how images can be scanned using the eight possible bidirectional scan patterns.
