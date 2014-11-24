---
layout: post
title: "Define.js, Combokeys"
author: "Alex Young"
image: "/images/posts/definejs.png"
categories:
- amd
- modules
- keyboard
---

###DefineJS

[DefineJS](http://fixjs.github.io/define.js/) (GitHub: [fixjs/define.js](https://github.com/fixjs/define.js), License: _MIT_, npm: [definejs](https://www.npmjs.org/package/definejs)) by Mehran Hatami is a new module loader.  It implements the AMD pattern and also supports Promised Modules, and other new nonstandard related module techniques.

You can specify the module's global name by including a `global` attribute on the script tag:

{% highlight html %}
<script global="definejs" src="define.js"></script>
{% endhighlight %}

Now you can declare a module with `definejs.define()` and load dependencies with `definejs.require`.  Promised modules are implemented by returning `new Promise` when declaring a dependency.

The author has included tests written with the Karma test runner, so you can run the tests against a real browser.

###Combokeys

Shahar Or sent in a keyboard shortcut library called Combokeys (GitHub: [mightyiam/combokeys](https://github.com/mightyiam/combokeys), License: _Apache 2.0_), a fork of the popular [Mousetrap](https://github.com/ccampbell/mousetrap) project.

It has some cool changes: it's been refactored to use CommonJS, and it doesn't automatically listen on `document`.  You can now specify which element it listens on for keyboard shortcuts.  That was actually one thing that prevented me from using Mousetrap in a project.
