---
layout: post
title: "Script Roundup: Handpicked jQuery, Firepoker, Enyo 2.3"
author: Alex Young
categories:
- jquery
- plugins
- angular
- apps
- cdn
---

<div class="intro">
Note: You can send your scripts and articles in for review through our <a href="/contact.html">contact form</a>.
</div>

###Handpicked jQuery Plugins

The [Handpicked jQuery Plugins](http://jque.re/) site by David Higgins has been updated to the third version.  He's also released [code.jque.re](http://code.jque.re/), which has links to resources served from MaxCDN.  All of the plugins have MaxCDN links as well.

> The site gets increasingly lean and mean over time. Outdated plugins get removed, and new ones take their place. The colors change, the CDN gets better, and more new fans download the repo each day to experiment with the plugins.

###Firepoker

![Firepoker](/images/posts/firepoker.png)

[Firepoker](http://firepoker.io/) (GitHub: [Wizehive / Firepoker](https://github.com/Wizehive/Firepoker), License: _MIT_) by Everton Yoshitani is a "Scrum poker" game used for estimating user stories.

> In planning poker, members of the group make estimates by playing numbered cards face-down to the table, instead of speaking them aloud. The cards are revealed, and the estimates are then discussed. By hiding the figures in this way, the group can avoid the cognitive bias of anchoring, where the first number spoken aloud sets a precedent for subsequent estimates.

It's built with AngularJS and [Firebase](https://www.firebase.com/).  It comes with a Grunt build script, so you can run a local development server to check it out easily.

The Firebase integration seems lightweight and easy to follow -- if you look at [main.js](https://github.com/Wizehive/Firepoker/blob/master/app/scripts/controllers/main.js) you can see how [AngularFire](https://github.com/firebase/angularFire) is used.

If you're looking for an AngularJS/Firebase example app, then take a look at the source for Firepoker.

###Let's Make a Framework Chronological List

Uri sent in a chronological list of the Let's Make a Framework posts, because DailyJS is really just a static site so sometimes it's a bit hard to make sense of long running article series:

<http://jsbin.com/AduboCI/2>

###Enyo 2.3.0

Ben Combee sent in a post about [Enyo 2.3.0-pre.10](http://blog.enyojs.com/post/64402443506/announcing-enyo-2-3-0-pre-10):

> If you've been following Enyo, you've probably noticed that it has been a while since our last public release. From the outside it may appear that the pace of Enyo development has slowed, but appearances can be deceiving — it has actually been an exceptionally busy, productive year for the Enyo team.

> So what have we been up to? For starters, we've been doing some exciting UI work to support an upcoming LG product release. We can't share this work with you just yet, but it will ultimately be open-sourced alongside our other Enyo libraries. We've also been pushing forward on the Ares IDE, with our HP team members playing a leading role.

Enyo 2.3 should improve data bindings, data layers, and adds the `enyo.Application` kind which is an entry point that can be used to organise data and functionality across the entire application.

The blog post explains how to get the prerelease and start using it.
