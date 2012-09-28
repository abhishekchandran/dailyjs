---
layout: post
title: "XLSX.js, Tres, ChromaNope"
author: "Alex Young"
categories: 
- mobile
- spreadsheets
- usability
---

###XLSX.js

[XLSX.js](http://blog.innovatejs.com/?page_id=7) (GitHub: [stephen-hardy / xlsx.js](https://github.com/stephen-hardy/xlsx.js), License: _Microsoft Office Extensible File License_) by Stephen Hardy can read and write Excel-compatible XLSX files.  It converts base64 strings into object representations of XLSX spreadsheets, without using ActiveX.

It's built using [JSZip](http://stuartk.com/jszip/), and will generate `data:` URIs with a base64 encoded string that contains the spreadsheet's XML.

###Tres

![Tres](/images/posts/tres.png)

[Tres](http://tres.io/) (GitHub: [juliocesar / tres](https://github.com/juliocesar/tres), License: _MIT_) by Julio Cesar Ody is a mobile framework based on Backbone.js.  It provides some convenience classes for working with touch-based gestures and the wide variety of mobile device resolutions, and enough CSS and icons to jump-start development.

Like Backbone.js, Tres has its roots in Rails, so initial versions aim to provide interfaces that work well with Ruby-based projects.  This includes console-based tools for generating stub files.

###ChromaNope

![ChromaNope](/images/posts/chromanope.png)

[ChromaNope](http://chromanope.com/) by [Kris Hedges](http://inkspeck.com/) is a web service designed to illustrate the effects of various forms of colour blindness.  It uses Node and PhantomJS to render any web page against the equivalent protanope, deuteranope, and tritanope version.  Definitions of these terms can be found on the [Wikipedia Color blindness](http://en.wikipedia.org/wiki/Protanope) page.
