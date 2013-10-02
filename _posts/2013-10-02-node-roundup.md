---
layout: post
title: "Node Roundup: 0.10.20, Asker, AbsurdJS"
author: "Alex Young"
categories: 
- node
- modules
- npm
- css
- http
---

###Node 0.10.20

[Node 0.10.20 is out](http://blog.nodejs.org/2013/09/30/node-v0-10-20-stable/) which means Node 0.10 is almost old enough to drink in most US states.  How about that!  This version fixes that annoying error that I seem to see when deploying to Heroku which reads: `npm ERR! cb() never called`.

###Asker

Asker (GitHub: [nodules / asker](https://github.com/nodules/asker), License: _MIT_, npm: [asker](https://npmjs.org/package/asker)) is a `http.request` wrapper with retries, gzip decoding, and connection pool tuning.  It was created by Phillip Kovalev for Yandex and is used on the [auto.yandex.ru](http://auto.yandex.ru/) site.

Asker isn't really a competitor to [request](https://npmjs.org/package/request), but a module designed around tailoring HTTP requests to comply with service level agreements.  It makes certain things easier, like body encoding.

Node's built-in HTTP connection pools are eschewed for a custom solution that allows you to prioritise services.  This helps avoid situations where a critical service fails due to the exhaustion of TCP sockets.  More is explained in the project's readme file, and the project includes unit tests as well.

###AbsurdJS

AbsurdJS (GitHub: [krasimir / absurd](https://github.com/krasimir/absurd), License: _MIT_, npm: [absurd](https://npmjs.org/package/absurd)) by Krasimir Tsonev is a CSS preprocessor that converts JSON to CSS:

{% highlight javascript %}
".navigation": {
  margin: "12px 0 0 0 ",
  type: "horizontal",
  a: {
    elementstyle: "button",
    responsive: "true"
  }
}
{% endhighlight %}

CSS isn't all that different from JSON when you think about it, but you can't easily include lumps of CSS in JavaScript files.  AbsurdJS allows you to sidestep this problem by converting JSON to CSS.  It includes a feature called _storage_ that allows you to define custom properties that will be expanded to standard CSS.

There's a detailed post about how it all works here: [Write Your CSS with JavaScript](http://davidwalsh.name/write-css-javascript).
