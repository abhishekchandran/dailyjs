---
layout: post
title: "Node Roundup: 0.11.7, 0.10.18, npm-check-updates, social-cms-backend"
author: "Alex Young"
categories: 
- node
- modules
- express
- npm
---

###Node 0.11.7, 0.10.18

Node [0.11.7](http://blog.nodejs.org/2013/09/04/node-v0-11-7-unstable/) and [0.10.18](http://blog.nodejs.org/2013/09/04/node-v0-10-18-stable/) were released last week.  The unstable branch has seen changes across many of the core modules, particularly `buffer` and `stream`.

Meanwhile, 0.10.8 has fixes for `stream` and updates uv.

###npm-check-updates

npm-check-updates (GitHub: [tjunnone / npm-check-updates](https://github.com/tjunnone/npm-check-updates), License: _Apache 2.0_, npm: [npm-check-updates](https://npmjs.org/package/npm-check-updates)) by Tomas Junnonen is a module for displaying out of date modules in your `package.json`.  It can also automatically update `package.json`.

I tried it against a few projects and it works OK, but it struggled with private repository URIs -- it just shows the 404 npm returns.

###social-cms-backend

social-cms-backend (GitHub: [dai-shi / social-cms-backend](https://github.com/dai-shi/social-cms-backend), License: _BSD_, npm: [social-cms-backend](https://npmjs.org/package/social-cms-backend)) by Daishi Kato is Express middleware that provides REST APIs for creating a social networks using AngularJS.

It uses [passport](https://npmjs.org/package/passport) for authentication, so it can work with various social networks.

Once it's installed you can set up persistence using MongoDB, and Facebook with passport's Facebook strategy:

{% highlight javascript %}
var express = require('express');
var SCB = require('social-cms-backend');
var app = express();
app.use(SCB.middleware({
  mongodb_url: 'mongodb://localhost:27017/socialcmsdb',
  passport_strategy: 'facebook',
  facebook_app_id: process.env.FACEBOOK_APP_ID,
  facebook_app_secret: process.env.FACEBOOK_APP_SECRET
}));
app.listen(3000);
{% endhighlight %}

