---
layout: post
title: "List.js, _part_"
author: "Alex Young"
categories: 
- libraries
- functional
---

###List.js

![List.js](/images/posts/listjs-logo.png)

Version 1.0 of [List.js](http://listjs.com/) (GitHub: [javve / list.js](https://github.com/javve/list.js), Bower: _javve/list.js_, License: _MIT_) by Jonny Strömberg has been released.  It's a small library for making tables searchable, sortable, and filterable.  It also works on unordered lists and divs, and supports templating so you can style it fairly easily.  It doesn't have any dependencies, and the API is straightforward JavaScript:

{% highlight javascript %}
listObj.add({ name: 'Jonny', city: 'Stockholm' });

listObj.add([
  { name: 'Gustaf', city: 'Sundsvall' }
, { name: 'Jonas', city: 'Berlin' }
]);
{% endhighlight %}

There are also [plugins for List.js](http://listjs.com/docs/plugins).  The project includes tests and can be installed with Bower or Component.

###The \_part\_ Library

[\_part\_](http://autosponge.github.io/blog/2013/11/27/_part_/) (GitHub: [AutoSponge / _part_](https://github.com/AutoSponge/_part_), License: _MIT_) by Paul Grenier is a small library for making native methods available as partially applied functions.

> In _part_, you use typical OO functions (like the ones in native prototypes) to create two functional counterparts, "left-part" and "right-part", which partially apply the receiver or parameters respectively.

While I was reading about this library I noticed the author has several other interesting posts on his blog:

* [Variadic Composition Without Recursion](http://autosponge.github.io/blog/2013/02/09/variadic-composition-without-recursion/)
* [Sparse Arrays For String Building](http://autosponge.github.io/blog/2012/09/22/sparse-arrays-for-string-building/)
* [Indexof Vs Regexp](http://autosponge.github.io/blog/2012/09/17/indexof-vs-regexp/)

