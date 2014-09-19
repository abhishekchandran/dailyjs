---
layout: post
title: "SVG Circus, Cheers"
author: "Alex Young"
categories:
- svg
- animation
- scraping
- dom
---

###SVG Circus

![SVG Circus](/images/posts/svgcircus.png)

[SVG Circus](http://svgcircus.com/) by Alex Kaul is a site for generating SVG animations.  You can use it to make spinners for loading indicators, or other animations if you get creative.

It's built with AngularJS and Bootstrap, and the Bootstrap customisation looks pretty cool.  Animations can be exported as XML with embedded JavaScript for animation.

###Cheers

Yesterday I mentioned [ineed](https://github.com/inikulin/ineed), a scraper API based around a streaming tokenizer.  Most of my Node scraping work has been written with [Cheerio](https://www.npmjs.org/package/cheerio), which is a small jQuery-inspired API for Node.  Cheers (GitHub: [fallanic / cheers](https://github.com/fallanic/cheers), License: _MIT_, npm: [cheers](https://www.npmjs.org/package/cheers)) by Fabien Allanic is a Cheerio-based scraper library:

> The motivation behind this package is to provide a simple cheerio-based scraping tool, able to divide a website into blocks, and transform each block into a JSON object using CSS selectors.

It works by using configuration objects that describe metadata based on CSS selectors, so it may help you to be more pragmatic about how you scrape documents.

