---
layout: post
title: "DefiantJS, Mprogress.js"
author: Alex Young
categories:
- json
- ui
- libraries
---

###DefiantJS

[DefiantJS](http://www.defiantjs.com/) (GitHub: [hbi99/defiant.js](https://github.com/hbi99/defiant.js), License: _MIT_) by Hakan Bilgin is a library for searching JSON documents with XPath expressions.

> Do you need to query large JSON structures? Do you end up coding loops to parse the JSON and identify the data that matches your query? DefiantJS offers a better way. DefiantJS extends the global JSON object with a "search" method that enables lightning-fast searches using XPath expressions.

It comes with something called "snapshot search" that allows you to quickly search large documents.  It's used like this:

{% highlight javascript %}
var snapshot = Defiant.getSnapshot(data);
// Snapshot search - this is more than 100 times faster than 'regular search'
found = JSON.search(snapshot, '//item');
{% endhighlight %}

You can also use DefiantJS to apply JSON to XSLT.  This may be useful if you have existing XSLT documents that you want to use with a newer JavaScript project.

The project's documentation has interactive examples that you can try out, so you can get a feel for how XPath expressions work.

###Mprogress.js

[Mprogress.js](http://lightningtgc.github.io/MProgress.js/) (GitHub: [lightningtgc/MProgress.js](https://github.com/lightningtgc/MProgress.js), License: _MIT_) is a Material Design-inspired progress bar.  It can display a progress bar at the top of the screen like Android applications, but you can also place it within other page elements as well.

It uses a simple constructor function called `Mprogress`, and you can start the progress indicator animation with `start`.  When the task has finished you call `end`:

{% highlight javascript %}
var mprogress = new Mprogress();
mprogress.start();
// Slow things happen here
mprogress.end();
{% endhighlight %}

It has other methods as well, like `set` for changing the position, and it supports video-style "buffering" indicators where two bars are used to show the current playback position and the point at which the data has been buffered.  The project's GitHub page has animated gifs that illustrate each of the animation types.
