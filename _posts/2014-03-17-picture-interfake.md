---
layout: post
title: "picturePolyfill, Interfake"
author: Alex Young
categories:
- json
- node
- modules
- html5
- polyfills
---

###picturePolyfill

[picturePolyfill](http://verlok.github.io/picturePolyfill/) (GitHub: [verlok / picturePolyfill](https://github.com/verlok/picturePolyfill), License: _MIT/GPL2_) by Andrea Verlicchi allows you to use `picture` elements with `srcset` support so you can include high-DPI images.  Here's an example with media queries:

{% highlight html %}
<picture data-alt="A beautiful responsive image" data-default-src="img/1440x1440.gif">
  <source src="img/480x480.gif"/>
  <source src="img/768x768.gif"   media="(min-width: 481px)"/>
  <source src="img/1440x1440.gif" media="(min-width: 1025px)"/>
  <source src="img/1920x1920.gif" media="(min-width: 1441px)"/>
  <noscript>
    <img src="img/768x768.gif" alt="A beautiful responsive image"/>
  </noscript>
</picture>
{% endhighlight %}

It doesn't make multiple HTTP requests, so only the required images are fetched.  It also takes into account browser event handling, so it won't run while the browser is being resized.

###Interfake

Interfake (GitHub: [basicallydan / interfake](https://github.com/basicallydan/interfake), License: _MIT_, npm: [interfake](https://www.npmjs.org/package/interfake)) by Daniel Hough is a module designed for client-side developers that makes it easy to create JSON APIs.  You can create APIs using the command-line interface by making JSON files that define endpoints:

{% highlight javascript %}
[{
  "request": {
    "url": "/whattimeisit",
    "method": "get"
  },
  "response": {
    "code": 200,
    "body": {
      "theTime": "Adventure Time!",
      "starring": [
        "Finn",
        "Jake"
      ],
      "location": "ooo"
    }
  }
}]
{% endhighlight %}

It supports JSONP, and you can use it programmatically in Node.  The documentation has some use-case ideas, like using it for a test API for a mobile application, automated testing, and static APIs.
