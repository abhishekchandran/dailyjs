---
layout: post
title: "Indentation"
author: Alex Young
categories:
- editing
- indentation
---

I like indenting with spaces, and it's partly due to the types of programming languages I use.  Some languages and styles depend on vertical alignment, so tabs and spaces end up getting mixed, which causes anything but a particular tab width to look weird.  That was the case in the Objective-C projects at the company I'm currently working at.

The [C++ programmer](https://twitter.com/gormlai) in our team loves tabs, however, and he pointed out [Elastic tabstops](http://nickgravgaard.com/elastictabstops/).  To understand how it works, take a look at the gif that shows code being edited as vertically aligned sections adapt automatically.  There are several implementations of this idea, including Visual Studio and Eclipse plugins.

Sindre Sorhus sent in [detect-indent](https://github.com/sindresorhus/detect-indent) which is a Node module for detecting and persisting indentation.  New text can be inserted with the correct indentation, and it can help configure your editor.

It also works in browsers, and can be installed with both Bower and Component.

Sindre's example uses JSON:

{% highlight javascript %}
var fs = require('fs');
var detectIndent = require('detect-indent');
/*
{
    "ilove": "pizza"
}
*/
var file = fs.readFileSync('foo.json', 'utf8');
// tries to detect the indentation and falls back to a default if it can't
var indent = detectIndent(file) || '    ';
var json = JSON.parse(file);

json.ilove = 'unicorns';

fs.writeFileSync('foo.json', JSON.stringify(json, null, indent));
/*
{
    "ilove": "unicorns"
}
*/
{% endhighlight %}
