---
layout: post
title: "ngKookies, preCode.js"
author: Alex Young
categories:
- cookies
- angularjs
- html
- dm
---

###ngKookies

ngKookies (GitHub: [voronianski/ngKookies](https://github.com/voronianski/ngKookies), License: _MIT_, npm: [ngkookies](https://www.npmjs.com/package/ngkookies)) by Dmitri Voronianski is a replacement for the Angular `$cookieStore` provider.  It's a port of [jquery-cookie](https://github.com/carhartl/jquery-cookie) that helps work around [angular.js issue 950](https://github.com/angular/angular.js/issues/950).

After loading it, you can set cookies with `$kookies.set('name', 'value')` and read them with `$kookies.get`.  You can also delete cookies with `$kookies.remove`.

Each method accepts an options object that can include the `path` and `expires` arguments.  You can also store JSON objects as cookies with `$kookiesProvider.config.json = true`.

###preCode.js

Have you ever written a blog engine or CMS that has to display source code?  If so you've probably run into the issue where human-readable HTML doesn't work well with `pre` elements if initial indentation is included.

[preCode.js](https://github.com/leeoniya/preCode.js) (License: _MIT_) Leon Sorokin is a small script that finds `<pre><code>` blocks and strips the leading and proceeding whitespace, so syntax highlighters should be able to display code properly.

It's written using the standard DOM API, so it shouldn't need any dependencies.  It'll also fix whitespace in `textarea` as well.
