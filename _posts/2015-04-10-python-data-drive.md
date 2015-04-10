---
layout: post
title: "Dreadnought, Data-Drive"
author: Alex Young
categories:
- python
- pyv8
- google
- libraries
---

###Dreadnought

If there's a Python library that you really want to use with no equivalent in Node, what do you do?  You could learn enough Python to get a Flask server running, but there's another option: run JavaScript from within Python!

[Dreadnought-js](https://sites.google.com/site/dreadnoughtjs/) (GitHub: [dschere/dreadnought-js](https://github.com/dschere/dreadnought-js), License: _MIT_) by David Schere uses [PyV8](https://code.google.com/p/pyv8/) to embed JavaScript into a Python web server.  The author prefers thinking of JavaScript as an embedded language, as it's used with browsers, and has aimed to provide seamless support with Python and C libraries.

> Dreadnought executes all HTTP requests within a separate child process launched by an internal web server allowing for synchronous programming using blocking calls without interfering with the main web service. This provides both fault tolerance and load balancing.

It naturally makes sense for Python programmers who want to use JavaScript, but I think it could also be useful for Node developers who want to use Python libraries for specific projects.

###Data-Drive

Ramon Gebben sent in Data-Drive (GitHub: [RamonGebben/data-drive](https://github.com/RamonGebben/data-drive), License: _MIT_), a library for reading and writing Google Spreadsheets.

Although there are other libraries that let you sign in to Google Spreadsheets and fetch data, Data-Drive has a feature that lets you map sheets.  You can create JSON descriptions of fields and values that will be used to convert the data when it's downloaded from the API.

Given something like this:

{% highlight javascript %}
"mapping": {
  "columns":[
    ["1", "key"],
    ["2", "key1"],
    ["3", "key2"]
  ]
}
{% endhighlight %}

You'll get:

{% highlight javascript %}
{
  "key": "pizza",
  "key1": "koffie",
  "key2": "kebeb",
  "id": 1
}
{% endhighlight %}

Which is way more convenient!
