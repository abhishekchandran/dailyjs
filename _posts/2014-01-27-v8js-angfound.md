---
layout: post
title: "v8js, Angular Foundation"
author: Alex Young
categories:
- php
- angular
- ui
---

###v8js

On Friday I wrote about [Uniter](http://dailyjs.com/2014/01/24/uniter-gamedev-chai/), which converts PHP to JavaScript.  But what about running JavaScript in PHP?  C. Scott Ananian sent in [v8js](http://pecl.php.net/package/v8js) (GitHub: [preillyme / v8js](https://github.com/preillyme/v8js), License: _MIT_), a PHP extension that lets you run JavaScript inside a PHP application.

It has both PHP and JavaScript APIs, so you can do things like `var_dump` in JavaScript.  In the PHP side, you can evaluate JavaScript with `$v8->executeString()`.

This project actually uses V8, and you can restrict JavaScript based on time and memory usage.

###Angular Foundation

![Angular Foundation](/images/posts/angularfoundation.png)

[Angular Foundation](http://madmimi.github.io/angular-foundation/) (GitHub: [madmimi / angular-foundation](https://github.com/madmimi/angular-foundation), License: _MIT_) is a [Foundation](http://foundation.zurb.com/) port of the AngularUI [bootstrap](https://github.com/angular-ui/bootstrap) project.

> We are aiming at providing a set of AngularJS directives based on Foundation's markup and CSS. The goal is to provide native AngularJS directives without any dependency on jQuery or Foundation's JavaScript. It is often better to rewrite an existing JavaScript code and create a new, pure AngularJS directive. Most of the time the resulting directive is smaller as compared to the orginal JavaScript code size and better integrated into the AngularJS ecosystem.

The documentation explains what Foundation components are supported, and shows how to use them as AngularJS directives.  The authors created it after they noticed people on Stack Overflow asking about AngularJS directives for Foundation, and finding the existing solutions less complete.
