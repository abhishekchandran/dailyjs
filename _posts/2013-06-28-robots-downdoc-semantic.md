---
layout: post
title: "RobotsConf, DownDoc, opensemanticapi"
author: Alex Young
categories:
- robots
- events
- markdown
- google
- node
---

###RobotsConf

![RobotsConf](/images/posts/robotsconf13.png)

[RobotsConf](http://robotsconf.com/) will take place on December 6th in Florida, and is a hardware-focused event aimed at developers who use high-level languages like JavaScript.  Organised by Chris Williams (aka [@voodootikigod](http://twitter.com/voodootikigod)), RobotsConf is a practical event to get you started in the Maker Movement:

> If you are a Ruby, Python, JS or any other high level language developer that is interested in the Maker Movement, but unsure where to start -- this event is designed for you. We will have experts in each high level language in attendance and available as well as many of the incredible makers who are already changing the world. With hands-on sessions covering drones, 3D Printing, microcontrollers, and the Internet of Things, this is the only two day event that will take you from a software developer to a Maker.

It's organised by the JSConf team, so you know you'll be in safe hands!  Tickets start at $550 for early birds, and then $750 for a regular ticket.

###DownDoc

If you followed my [Backbone.js Google Tasks tutorials](http://dailyjs.com/tags#backgoog) then you'll know all about the wonders of `gapi`.  [DownDoc](http://marksteve.com/downdoc/) (GitHub: [marksteve / downdoc](https://github.com/marksteve/downdoc), License: _MIT_) by Mark Steve Samson uses another Google API to store Markdown documents in Google Drive.  If you're tired of working with Word-like documents, then why not give it a try?  It's entirely browser-based, and the original source is pretty much a single CoffeeScript file.

###opensemanticapi

opensemanticapi (GitHub: [monbro / opensemanticapi](https://github.com/monbro/opensemanticapi), License: _MIT_) by Michael Klein is a "semantic wording database" made with Node and Redis.  After leaving it running for a few hours it will have downloaded enough data to produce interesting results.  Michael has some examples in the project's readme, for example:

{% highlight javascript %}
// http://localhost:8080/relations/ship

["midshipmen", "aboard", "ships", "rating", "master", "served", "seaman", "sea", "officers", "santa", "sailing", "cadets", "able", "sail", "navigation", "lieutenant", "hms", "expected", "yahoo", "storm", "rated", "promotion", "maría", "lewis", "false", "era", "boys", "wind", "voyage", "volunteer", "servants", "required", "passing", "palos"]
{% endhighlight %}

One thing that interests me about this is as a brainstorming tool for authors, as an alternative to a thesaurus.
