---
layout: post
title: "BindingJS, 2D Space Shooter Part 2"
author: "Alex Young"
image: "/images/posts/howtomakeaspaceshooter2.png"
categories:
- data-binding
- reactive
- libraries
- tutorials
- games
---

###BindingJS

[BindingJS](http://bindingjs.org/) (GitHub: [rummelj / bindingjs](https://github.com/rummelj/bindingjs), License: _MPL_) by Johannes Rummel is a data binding library that seeks to separate data binding declarations from HTML.  It has a Less-inspired syntax for defining bindings, which you can put in a `script` element with the `text/binding` type.

JavaScript is used to set things up, and the API is fluent, so you can chain calls to configure things like the template fragment that a binding document applies to.

The binding syntax is similar to CSS, but because it's influenced by Less you'll find it easier to group properties with nesting.

Data is accessed through "adapters", so it's fairly easy to customise it to existing applications:

> There are multiple view adapter such as value, text, attr or on that are already included in BindingJS. The qualifier of an adapter is a static instruction for the Adapter and is written directly behind the prefix, if that is only one character long. Otherwise it is separated by a colon from the prefix.

I like the idea of a CSS selector data binding language, but the expressions it uses are terse so it may take some effort to get the hang of BindingJS.  Also, I think it would work well with [custom elements](http://www.html5rocks.com/en/tutorials/webcomponents/customelements/), so it would be worth experimenting with that.

###Part 2 of How to Make a 2D Space Shooter in Unity

Thomas Palef sent in [part 2 of How to Make a 2D Space Shooter in Unity](http://blog.lessmilk.com/unity-spaceshooter-2/).  This is the tutorial series that uses Unity's JavaScript API.  In this part Thomas adds enemies and collision handling as well.
