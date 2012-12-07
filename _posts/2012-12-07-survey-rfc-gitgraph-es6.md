---
layout: post
title: "JavaScript Survey 2012, Gitgraph, ES6 Proxies"
author: Alex Young
categories: 
- ES6
- git
- graphs
- Canvas
- survey
- community
---

###JavaScript Survey 2012: RFC

I'm currently researching the next JavaScript Developer Survey.  I'd like feedback on questions.  If there's anything you'd strongly like to see in the survey, please [contact me](http://contact.dailyjs.com/general) and I'll see if I can incorporate it.

Previous surveys can be found here:

* [JavaScript Developer Survey 2011](http://dailyjs.com/2011/12/15/javascript-survey-results)
* [JavaScript Developer Survey 2010](http://dailyjs.com/2010/12/13/javascript-survey-results/)
* [JavaScript Developer Survey 2009](http://dailyjs.com/2009/12/02/survey-results)

In general, the surveys try to determine:

* How many readers are client-side or server-side developers
* Whether or not readers write tests
* Other languages used (C#, Java, Objective-C, PHP, Ruby, Python, etc.)

It's not necessarily used to design content for DailyJS -- the results are shared with the community benefit everyone.

###Gitgraph

[Gitgraph](http://bitpshr.info/gitgraph/) (GitHub: [bitpshr / Gitgraph](https://github.com/bitpshr/Gitgraph), License: _WTFPL_) by Paul Bouchon is a Canvas-based GitHub participation graph library.  It's based around a constructor function that accepts arguments for things like GitHub username, width, height, and colours:

{% highlight javascript %}
var graph = new Gitgraph({ 
    user        : 'nex3',                // any github username
    repo        : 'sass',                // name of repo
    domNode     : document.body,         // (optional) DOM node to attach to 
    width       : 800,                   // (optional) graph width
    height      : 300,                   // (optional) graph height
    allColor    : "rgb(202, 202, 202)",  // (optional) color of user's participation
    userColor   : "rgb(51, 102, 153)",   // (optional) color of total participation
    background  : "white",               // (optional) background styles
    showName    : true                   // (optional) show or hide name of user / repo
});
{% endhighlight %}

The author wrote some background on it in [GitHub Graphs Fo' Errbody](http://bitpshr.github.com/blog/2012/11/30/github-graphs-fo-errbody/), because he had to wrap missing API functionality with a proxy.

###Multiple Inheritance in ES6 with Proxies

[Multiple Inheritance in ES6 with Proxies](http://blog.avd.io/posts/multiple-inheritance) is an introduction to ES6 proxies by Jussi Kalliokoski.  The author's example uses `EventEmitter`, which I find useful because multiple inheritance with `EventEmitter` is something I've seen typically implemented using a for loop to copy properties.

The `Proxy` solution isn't far off that approach and requires more code, but it's worth reading if you're struggling to understand proxies.

