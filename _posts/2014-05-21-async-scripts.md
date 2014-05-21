---
layout: post
title: "Script-injected Async Scripts Considered Harmful"
author: Alex Young
categories:
- async
- performance
---

Ilya Grigorik has published a post about how script-injected resource loading could negatively impact performance, in [Script-injected "async scripts" considered harmful](https://www.igvita.com/2014/05/20/script-injected-async-scripts-considered-harmful/).

> The inline JavaScript solution has a subtle, but very important (and an often overlooked) performance gotcha: inline scripts block on [CSSOM](http://dev.w3.org/csswg/cssom/) before they are executed. Why? The browser does not know what the inline block is planning to do in the script it is about to execute, and because JavaScript can access and manipulate the CSSOM, it blocks and waits until the CSS is downloaded, parsed, and the CSSOM is constructed and available.

The example in the article shows a CSS download blocking script execution, where the scripts are short snippets that inject additional `script` elements to load real JavaScript files.  The delay of execution causes the files to be downloaded later than desired.

If you look at the source to DailyJS you can see Disqus injecting a script that way, and when I look at the network tab in Chrome Developer Tools it seems like `count.js` executes after the CSS files have downloaded.

The obvious fix is to use `async` attributes on `script` tags, as long as you can live with the additional effort to support IE8 and 9.  But before you rush off to reformat your sites, the last point by Ilya is interesting:

> Wait, should I just move all of my JavaScript above the CSS then? No. You want to keep your `<head>` lean to allow the browser to discover your CSS and begin parsing the actual page content as soon as possible - i.e. optimize the content you deliver in your first round trip to enable the fastest possible page render.

Optimising for all possible browser behaviours is difficult!
