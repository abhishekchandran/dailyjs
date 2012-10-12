---
layout: post
title: "Red Dwarf, Stately.js, ansi_up"
author: Alex Young
categories:
- github
- fsm
- console
---

###Red Dwarf

![Red Dwarf](/images/posts/reddwarf.png)

[Red Dwarf](http://jrvis.com/red-dwarf/) (GitHub: [rviscomi / red-dwarf](https://github.com/rviscomi/red-dwarf), License: _MIT_) by Rick Viscomi is a heat map visualisation of GitHub repository stars.  It can display stars for a specific repository, so [the joyent/node heat map](http://jrvis.com/red-dwarf/node/) is pretty interesting given the sheer amount of stars it has.

Google Maps is used for geocoding and displaying the map, and GitHub supplies the raw data.  Both of these APIs are accessible with client-side JavaScript, so the whole thing can work purely in-browser.  The visualisation itself is drawn using [Heatmap Layer](https://developers.google.com/maps/documentation/javascript/layers#JSHeatMaps), provided by Google Maps.

###Stately.js

![Stately.js logo](/images/posts/statelyjs.png)

[Stately.js](https://github.com/fschaefer/Stately.js) (License: _MIT_) by Florian Schäfer is a finite-state automaton engine, suitable for use in client-side projects.  Given that most of us are used to working with events, state machines work quite naturally in JavaScript.  Stately.js allows transitions to be tracked using notifications, and handlers can be registered and removed as required.

Florian's documentation is detailed, and the "door" example is an easy one to follow if you're confused about how the project can be used.  Some simple tests have also been included, with a small HTML test harness.

###ansi_up

![ansiup example](/images/posts/ansiup.png)

I still hang out in IRC, and I still like using Mutt for email.  There's something reassuring about the glare of colourful text-based interfaces that no GUI will ever replace.  If you're a fellow console hacker, then you may find a use for [ansi_up](https://github.com/drudru/ansi_up) (License: _MIT_, npm: [ansi_up](https://npmjs.org/package/ansi_up)) by Dru Nelson.  It converts text with ANSI terminal colour commands into HTML, so you can take your FIGlet-powered nonsense to the web and annoy people with it there.

Dru says this project has been used "in production" since early 2012 -- I wonder what it's being used for?
