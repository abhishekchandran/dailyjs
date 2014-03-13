---
layout: post
title: "Multiline strings in JavaScript"
author: Alex Young
categories:
- es6
- hacks
---

Multiline (GitHub: [sindresorhus / multiline](https://github.com/sindresorhus/multiline), License: _MIT_, npm: [multiline](https://www.npmjs.org/package/multiline)) by Sindre Sorhus is a clever hack that allows you to write multiline strings by using a callback to wrap around a comment:

{% highlight javascript %}
var str = multiline(function(){/*
<!doctype html>
<html>
    <body>
        <h1>❤ unicorns</h1>
    </body>
</html>
*/});
{% endhighlight %}

This works by calling `.toString()` on the callback, then running a regular expression to extract the comment: `/\/\*!?(?:\@preserve)?\s*(?:\r\n|\n)([\s\S]*?)(?:\r\n|\n)\s*\*\//`.

Although this is a hack, I hadn't thought about it before.  Sindre notes that this has a performance impact, but that sometimes it might be worth writing things this way for the added clarity it brings.

EcmaScript 6 will introduce [template strings](http://tc39wiki.calculist.org/es6/template-strings/), which can be used for multiline strings and interpolation with {% raw %}`${}`{% endraw %}:

> A template string uses back ticks instead of double quotes or single quotes. The template string can contain place holders, which use the {% raw %}`${ }`{% endraw %} syntax. The value of the expressions in the place holders as well as the text between them gets passed to a function. This function is determined on the expression before the template string. If there is no expression before the template string the default template string is used.


