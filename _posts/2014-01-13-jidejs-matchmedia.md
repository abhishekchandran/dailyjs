---
layout: post
title: "jide.js, Matchmedia-ng"
author: Alex Young
categories:
- angularjs
- ui
- matchMedia
---

###jide.js

[jide.js](http://js.jidesoft.com/) (GitHub: [jidesoft / jidejs](https://github.com/jidesoft/jidejs), License: _MIT_) from JIDE Software is a toolkit for HTML5 UI controls.  The authors have embraced RequireJS, and the API is based around constructor functions that accept objects.  Properties and values are observable, so UI components can react to data model changes.  Layouts are also supported, which are stackable panes reminiscent of desktop UI toolkits.

There are tutorials for using jide.js with [Bower](http://js.jidesoft.com/guide/00-installation/02-with-bower.html) and [Yeoman](http://js.jidesoft.com/guide/00-installation/03-with-yeoman.html), so if you want to create a quick project you can type `npm install -g generator-jidejs` and then `yo jidejs`.

Here's an example of how to create a button with jide.js:

{% highlight javascript %}
require([
  'jidejs/ui/control/Button'
], function(Button) {
  new Button({
    // define the text property
    text: 'Click the button',
    // define event listeners
    on: {
      // the 'action' event is fired when the button is clicked
      action: function() {
        alert('Hello jide.js');
      }
    }
  });
});
{% endhighlight %}

###Matchmedia-ng

[Matchmedia-ng](http://analogj.github.io/matchmedia-ng/) (GitHub: [AnalogJ / matchmedia-ng](https://github.com/AnalogJ/matchmedia-ng), License: _MIT_) by Jason Kulatunga is a set of AngularJS bindings for `window.matchMedia`.  That means you can easily branch on mobile devices, or for printed content:

{% highlight javascript %}
matchmedia.on('tv and (min-width: 700px) and (orientation: landscape)', function(mediaQueryList) {
  console.log(mediaQueryList.matches);
});
{% endhighlight %}

There's also a [matchMedia polyfill](https://github.com/paulirish/matchMedia.js/) written by Paul Irish.

