---
layout: post
title: "ng-polymer-elements, Easy CSS Animations"
author: "Alex Young"
categories:
- libraries
- graphics
- animation
- angularjs
- polymer
---

###ng-polymer-elements

ng-polymer-elements (GitHub: [GabiAxel / ng-polymer-elements](https://github.com/GabiAxel/ng-polymer-elements), License: _MIT_) by Gabriel Axel is a library for mapping between AngularJS models and Polymer data-bindings.

It comes with support for various components, including `core-input`, `paper-input`, `paper-checkbox`, and `paper-toast`.  As an example, binding the Angular scope's `myText` property to Polymer's `paper-input` looks like this:

{% highlight html %}
<paper-input ng-model="myText"></paper-input>
{% endhighlight %}

You can extend the supported components by adding mappings to `window.NG_POLYMER_ELEMENTS_EXTENDED_MAPPINGS`.  There's an example of this in the readme.

###Easy CSS Animations

<img src="https://s3.amazonaws.com/store-production-images/blog/papers-animations-css.gif" width="530" />

Erica Salvaneschi wrote [Easy CSS Animations](http://blog.papersapp.com/easy-css-animations/), which demonstrates how to animate illustration-based web designs with CSS.  The animations are subtle but interesting -- I like the ones that persist after the initial page load.

> CSS animations are an excellent way to make web pages look cool with relatively little effort. We used animations in our recent Windows Beta release page to bring our designer's creative doodles to life. Since then we've released Papers 3 for Windows and created more pages with subtle animations.

> We've extracted the CSS for you and shared it in this GitHub repository: [mekentosj/blog-windows-animations](https://github.com/mekentosj/blog-windows-animations).

She's included some tips about using Retina.js, and basic drawing with CSS borders.
