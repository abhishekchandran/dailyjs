---
layout: post
title: "Ditto, sudo.js, dry-observer"
author: "Alex Young"
categories: 
- mvc
- backbone.js
- dojo
- libraries
---

###Ditto

[Ditto](http://bitpshr.info/ditto/) (GitHub: [bitpshr / ditto](https://github.com/bitpshr/ditto), License: _WTFPL_) by Paul Bouchon is a tool for resolving a project's Dojo dependencies.  A project's zip file can be dropped onto the site, and it will analyse it and extract all of the required AMD modules.  There's an options tab that has an option for the legacy `dojo.require` syntax, and paths can be ignored as well.

###sudo.js

[sudo.js](https://github.com/robrobbins/sudo-js) (License: _MIT_, npm: [sudoclass](https://npmjs.org/package/sudoclass)) by Rob Robbins (sent in by Yee Lee) is a library that features inheritance helpers, view and view controllers, and data binding support.  The API is documented in the [sudo.js wiki](https://github.com/robrobbins/sudo-js/wiki).

The author has included a test suite, compatibility polyfills for things like the `console` object and `String.prototype.trim`, and an optional build with a small templating library.

###dry-observer

[dry-observer](https://github.com/arbales/dry-observer) (License: _MIT_) by Austin Bales is a small library for working with centralising binding and unbinding to events, while encouraging consistent handler naming.  It requires a Backbone.js or at least a `Backbone.Events`-compatible object.

Here's a quick example by the author:

{% highlight coffeescript %}
# Observe a Model by passing a hash…
@observe model,
  'song:change'   : @onSongChange
  'volume:change' : @onVolumeChange
  'focus'         : @onFocus

# …or a String or Array.
# Observation will camelCase and prefix your events.
@observe model, 'song:change volume:change focus'

# Stop observing and dereference your model…
@stopObserving model

# …or stop observing /everything/
@stopObserving()
{% endhighlight %}
