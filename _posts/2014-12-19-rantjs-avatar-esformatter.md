---
layout: post
title: "Rantjs, Avatar, esformatter"
author: Alex Young
categories:
- text
- graphics
- atom
- plugins
---

###Rantjs

[Rantjs](http://rantjs.robbestad.com/) (GitHub: [svenanders/Rantjs](https://github.com/svenanders/Rantjs), License: _ISC_, npm: [rantjs](https://www.npmjs.com/package/rantjs)) by Sven Anders Robbestad is a library for procedurally generating text.  It takes a formatted constructor and then generates suitable sentences:

{% highlight javascript %}
var rantjs = require('rantjs');
var rant = new rantjs.SimpleRant;
var sentence = rant.rantConstructor('<firstname male> likes to <verb-transitive> <noun.plural> with <pron poss male> pet <noun-animal> on <timenoun dayofweek plural>.');

console.log(sentence); // 'Sean likes to chop parrots with his pet cat on Saturdays.'
{% endhighlight %}

There are a lot of supported tags, with subgroups, so you can generate a `activity video` or `adv emotion`.  You can also add your own tags.

The author suggests that this might be useful for generating random text in games, but I think it might also work well for generating random admin area sample text in a blog or CMS, and for creating text to use in testing.

###Avatar

If you're looking for a way to generate default avatars, then take a look at [Avatar](http://matthewcallis.github.io/avatar/) (GitHub: [MatthewCallis/avatar](https://github.com/MatthewCallis/avatar), License: _MIT_, npm: [avatar-initials](https://www.npmjs.com/package/avatar-initials)) by Matthew Callis.  It can show the user's initials in a styled or unstyled avatar, or optionally fall back to a Gravatar instead.

To use it, just instantiate `Avatar` with the container element:

{% highlight javascript %}
var avatar = new Avatar(document.getElementById('avatar'), {
  useGravatar: false,
  initials: 'MC'
});

/* or */

$('#avatar').avatar({
  useGravatar: false,
  initials: 'MC'
});
{% endhighlight %}

###esformatter

Sindre Sorhus sent in [atom-esformatter](https://atom.io/packages/esformatter) (GitHub: [indresorhus/atom-esformatter](https://github.com/sindresorhus/atom-esformatter), License: _MIT_), an Atom editor package for formatting JavaScript with [esformatter](https://github.com/millermedeiros/esformatter).  Esformatter itself supports lots of options for formatting JavaScript, like the indentation characters, line breaks, and whitespace handling.

Sindre's Atom package lets you run esformatter from the Command Palette by typing `esformatter`, and you can run it on a selection or the whole file.

Esformatter supports plugins, so you can change its behaviour by loading other Node modules.  There's a [list of plugins](https://github.com/millermedeiros/esformatter/wiki/Plugins) and also a plugin wish list.  Sindre notes that it can be used with Gulp and Grunt, which might be a good way of processing open source JavaScript according to your project's style guide before you release it.
