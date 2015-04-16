---
layout: post
title: "Free js.org Subdomains, Wallpaper"
author: Alex Young
categories:
- node
- modules
- npm
- libraires
- hosting
- desktop
---

###Free js.org Subdomains

Stefan Keim wanted to give something back to the JavaScript community, so he's started [js.org](http://dns.js.org) -- a service that provides free subdomains for JavaScript programmers.  You can host your project on GitHub, then point a `js.org` subdomain at it.

To claim a subdomain you need to do three things:

1. Create your [GitHub Pages](https://pages.github.com)-hosted site
2. Add a CNAME file to your repository with the `js.org` name that you want
3. Make a pull request to [GitHub: js-org/dns](https://github.com/js-org/dns/) that adds your CNAME to the list

Given how valuable the `js.org` domain is I think this is very generous of Stefan, and the GitHub-based approach is a nice idea as well.

###Wallpaper

Sindre Sorhus sent in wallpaper (GitHub: [sindresorhus/wallpaper](https://github.com/sindresorhus/wallpaper), License: _MIT_, npm: [wallpaper](https://www.npmjs.com/package/wallpaper)), a module for changing the desktop wallpaper in Mac OS X, Linux, and Windows.

It has a command-line tool (`wallpaper [file]`) and a Node API:

{% highlight javascript %}
var wallpaper = require('wallpaper');

wallpaper.set('unicorn.jpg', function(err) {
 console.log('done');
});

wallpaper.get(function(err, imagePath) {
  console.log(imagePath);
  //=> '/Users/sindresorhus/unicorn.jpg' 
});
{% endhighlight %}

It would be great to combine this with a Node Canvas module that generates data-driven art, or maybe even using PhantomJS to render a webpage to recreate the joys of Active Desktop!
