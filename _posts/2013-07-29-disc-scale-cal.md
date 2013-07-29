---
layout: post
title: "Disc, scaleApp, Cal-HeatMap"
author: Alex Young
categories:
- browserify
- ui
- graphs
- frameworks
- libraries
- modules
- node
---

###Disc

![Disc](/images/posts/disc.png)

[Disc](http://hughsk.github.io/disc/) (GitHub: [hughsk / disc](https://github.com/hughsk/disc), License: _MIT_, npm: [disc](https://npmjs.org/package/disc)) by Hugh Kennedy is a tool for generating interactive views of [browserify](http://browserify.org/) project bundles:

> It's especially handy for catching large and/or duplicate modules which might be either bloating up your bundle or slowing down the build process. It works with node projects too!

Running `disc index.js > stats.html` will generate a file that uses [D3.js](http://d3js.org/) to display two visualisations: file count and file size.  It's a little bit like the file system usage applications for desktop systems.

###scaleApp

Markus Kohlhase has been quietly working on a project called [scaleApp](http://www.scaleapp.org/) (GitHub: [flosse / scaleApp](https://github.com/flosse/scaleApp), License: _MIT_, npm: [scaleapp](https://npmjs.org/package/scaleapp)) -- a framework for creating single page applications.  It's designed to help you write decoupled, event-driven apps, and is influenced by Nicholas C. Zakas's talk [Scalable JavaScript Application Architecture](https://www.youtube.com/watch?v=vXjVFPosQHw).

The project has no dependencies and supports Node and browsers.  AMD and CommonJS modules are both supported, and it can be extended with plugins.  There are already plugins for internationalisation, DOM manipulation, MVC, and more.

Applications are based around modules, which are registered and "started".  Multiple instances of a module can be started, and they talk to each other using a pub/sub API.  Flow control for asynchronous methods is also possible, with the `runSeries` and `runWaterfalladdressed` methods.

Projects are deployed to browsers by using "browser bundles" -- Grunt is used as the build system.  There is a [scaleApp demo application](http://www.scaleapp.org/readme.html#demo) ([source](https://github.com/flosse/FAST)), so you can see what a real application built with the framework looks like.

###Cal-HeatMap

![Cal-HeatMap](/images/posts/calheatmap.png)

[Cal-HeatMap](http://kamisama.github.io/cal-heatmap/) (GitHub: [kamisama / cal-heatmap](https://github.com/kamisama/cal-heatmap), License: _MIT_, Bower: _cal-heatmap_) is a GitHub-style calendar heatmap created by Wan Qi Chen.  It uses D3.js, and comes with a build script and tests.

{% highlight javascript %}
var cal = new CalHeatMap();
cal.init({
  start: new Date(2000, 0),
  range: 12,
  domain: 'year',
  subDomain: 'month',
  data: 'http://example.com/api.json'
});
{% endhighlight %}

Data can be loaded remotely, and CSV, JSON, TSV, and plain text formats are supported.  The API allows values to be highlighted, and the legend, cell size, and position are all configurable.

