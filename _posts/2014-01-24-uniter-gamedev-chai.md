---
layout: post
title: "Uniter, Chai Webdriver, Gamedev.js Weekly"
author: Alex Young
categories:
- php
- testing
- games
---

###Uniter

When we run our [yearly survey](http://dailyjs.com/tags.html#surveys), I've noticed PHP is popular with our readers.  So here's something that you might either love, or consider arcane blasphemy: [Uniter](http://asmblah.github.io/uniter/demo/interactive.html) (GitHub: [asmblah / uniter](https://github.com/asmblah/uniter), License: _MIT_), a JavaScript to PHP source-to-source compiler:

> Uniter allows you to execute PHP in the browser or in Node.js.  As an on-the-fly recompiling interpreter (or transpiler) it results in the closest possible translation from PHP to native JavaScript code.

It includes Mocha unit tests and should run in IE 9 or above.  It currently supports most of PHP's keywords, and even has basic `class` support.  The demo is interactive, so you can try editing the PHP source to see what happens.

###Chai Webdriver

[Chai Webdriver](http://bites.goodeggs.com/open_source/chai-webdriver/) (GitHub: [goodeggs / chai-webdriver](https://github.com/goodeggs/chai-webdriver), License: _MIT_, npm: [chai-webdriver](https://npmjs.org/package/chai-webdriver)) by Max Edmands is a Chai plugin for making markup-based assertions when using webdriver.  For example:

{% highlight javascript %}
// Start with a webdriver instance:
var sw = require('selenium-webdriver');
var driver = new sw.Builder()
  .withCapabilities(sw.Capabilities.chrome())
  .build()

// And then...
var chai = require('chai');
var chaiWebdriver = require('chai-webdriver');
chai.use chaiWebdriver(driver);

// And you're good to go!
driver.get('http://github.com');
chai.expect('#site-container h1.heading').dom.to.not.contain.text("I'm a kitty!");
{% endhighlight %}

It works with Selenium, chromedriver, PhantomJS, and SauceLabs.

###Gamedev.js Weekly

[Gamedev.js Weekly](http://weekly.gamedevjs.com/) is a weekly newsletter of JavaScript game-related news.  There's an [archive](http://weekly.gamedevjs.com/archive.html) so you can preview it before signing up.
