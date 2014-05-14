---
layout: post
title: "Node Roundup: Newman, selenium-test-runner, ncc"
author: "Alex Young"
categories:
- node
- modules
- npm
- chrome
- http
- testing
---

###Newman

Newman (GitHub: [a85 / Newman](https://github.com/a85/Newman), License: _Apache_, npm: [newman](https://www.npmjs.org/package/newman)) by Prakhar Srivastav is a command-line collection runner for [Postman](http://getpostman.com), the HTTP client for Chrome.

Newman allows you to easily run a collection, like this:

{% highlight javascript %}
newman -u https://www.getpostman.com/collections/cb208e7e64056f5294e5 -e devenvironment.json
{% endhighlight %}

In this example, `-e` is used to supply a JSON file that has configuration options for Postman's environment.  Newman's readme has more examples and documentation.

###selenium-test-runner

selenium-test-runner (GitHub: [tkambler / selenium-runner](https://github.com/tkambler/selenium-runner), License: _MIT_) by Tim Ambler is a library for writing Selenium tests in a blocking style.  It uses [node-fibers](https://github.com/laverdet/node-fibers) so you can avoid promises and chained expressions.

###ncc

![ncc](/images/posts/ncc.png)

ncc, or node-crome-canvas, (GitHub: [indus / ncc](https://github.com/indus/ncc), License: _MIT_, npm: [ncc](https://www.npmjs.org/package/ncc)) by Stefan Keim, uses the Chrome remote debugging protocol to build a bridge to the native HTMlCanvasElement and its 2d-Context.  That means you can send drawing operations from the server to Chrome.

Here's an example:

{% highlight javascript %}
var ncc = require('ncc')

var canvas = ncc();

canvas.width = canvas.height = 256;

var ctx = canvas.getContext('2d');

ctx.fillStyle = 'slateGray';
ctx.fillRect(28, 28, 200, 200)();
{% endhighlight %}
