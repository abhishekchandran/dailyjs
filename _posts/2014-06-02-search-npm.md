---
layout: post
title: "Searching npm"
author: Alex Young
categories:
- npm
- node
---

[My book](http://manning.com/young) is currently going through technical proof reading, so I've been getting lots of interesting feedback.  One small thing the reviewer noted was that `npm search express` generates thousands of results, so he asked how to filter the results.

The documentation for [npm search](https://www.npmjs.org/doc/cli/npm-search.html) shows that queries can use regular expressions.  In my shell I have to escape regular expressions with single quotes.  That means I can search for packages that start with "express" like this:

{% highlight text %}
npm search '/^express/'
{% endhighlight %}

That reduces the output to 623 results.  Perhaps, however, the issue was really relevance.  Lots of results aren't so bad if they're sorted in a reasonable way.  I tried [npmsearch](https://www.npmjs.org/package/npmsearch) which you can install with `npm install npmsearch`, and the results seemed very friendly.  You can even control the output with options like `--freshness` and `--aging`.

There's also [nipster](http://nipstr.com/), which combines npm's results with GitHub.  It feels fast, but it's actually a pretty simple client-side project.

Another thing to note is npm's standard search combines various fields (description, keywords, url) to create keywords, so you can't easily search on a specific field (unless I'm mistaken).  I'd like to search for something like [name:express](https://www.npmjs.org/search?q=name%3Aexpress), but I can't do that yet.

If you have any cool npm search-related tricks, please let me know!
