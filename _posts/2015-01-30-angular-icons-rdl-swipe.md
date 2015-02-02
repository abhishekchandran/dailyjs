---
layout: post
title: "Material Design Icons, rdljs, PhotoSwipe"
author: Alex Young
image: "/images/posts/angularmaterial.png"
categories:
- ui
- icons
- graphics
- microsoft
- images
---

###Material Design Icons for Angular

Google's Material Design stuff is amazing, and their recent UI and animation libraries are useful for those of us who don't want to spend too much time developing a totally new UI for every project.  However, these tools have limitations.  Urmil Parikh found that the official [Material Design Icons](https://github.com/google/material-design-icons) were hard to recolour without patching the SVG files.

![Material Design Icons](/images/posts/angularmaterial.png)

To work around this issue, Urmil created [Angular Material Icons v0.3.0](https://klarsys.github.io/angular-material-icons/) (GitHub: [klarsys/angular-material-icons](https://github.com/klarsys/angular-material-icons), License: _MIT_, Bower: `angular-material-icons`, npm: [angular-material-icons](https://www.npmjs.com/package/angular-material-icons)).  By including this project, you get a new Angular directive called `ng-md-icon` which supports options for style and size.  It also optionally supports [SVG-Morpheus](https://github.com/alexk111/SVG-Morpheus) -- this allows you to morph between icons which might work well in animation-heavy material design projects.

This library works by hard-coding the SVG paths in an object called `shapes`.  The paths can be embedded in `svg` elements with the required size and style attributes.

###rdljs

André Vale sent in [rdljs](https://github.com/andreventuravale/rdljs), a library for Microsoft RDL/RDLC reporting.  This technology is completely new to me, so I had to ask him for clarification.  Apparently, RDL stands for [Report Definition Language](http://en.wikipedia.org/wiki/Report_Definition_Language), and is used with Microsoft SQL Server Reporting Services.  RDL files are XML schemas for designing reports, so André's library allows you to take RDLC files and render them in a browser.

The library comes with a demo, but you'll need to run a webserver to try it out. It's intended to be used with a server side application that sends the XML using Ajax requests. It uses D3 and jQuery.  The source that does the XML parsing looks extremely involved, so it would be interesting to see what people can do with it who've got RDL experience.

###PhotoSwipe

[PhotoSwipe](http://photoswipe.com/) (GitHub: [dimsemenov/PhotoSwipe](https://github.com/dimsemenov/PhotoSwipe), License: _MIT_, Bower: `photoswipe`) by Dmitry Semenov is a mobile-friendly image gallery.  It works through instances of the `PhotoSwipe` object, and there are methods for things like going to the next/previous slide, and skipping to a specific slide.  The API also supports events.

There's full documentation in [website/documentation/api.md](https://github.com/dimsemenov/PhotoSwipe/blob/master/website/documentation/api.md) which explains how to add slides dynamically, so you can load slide data asynchronously if required.

One thing I liked about the PhotoSwipe was the mouse gestures: if you click and swipe it works in a similar way to swiping on a touchscreen.  It also feels fast and lightweight.
