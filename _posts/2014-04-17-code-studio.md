---
layout: post
title: "Browser Synths with Code Studio"
author: "Alex Young"
categories:
- node
- modules
- audio
---

<div class="image">
  <img src="/images/posts/codestudio.png" />
  <small>Code Studio running <a href="http://studio.substack.net/polytropon?time=1397235711071">polytropon</a>.</small>
</div>

[Code Studio](http://studio.substack.net/) (GitHub: [substack / code-music-studio](https://github.com/substack/code-music-studio), License: _MIT_, npm: [code-music-studio](https://www.npmjs.org/package/code-music-studio)) by substack is a tool for "designing musical algorithms".  It provides a browser-based interface that allows you to return functions that manipulate amplitudes.  You can experiment and share sounds using [studio.substack.net](http://studio.substack.net/), or install it with npm and run it locally.

If you want to find some code to play with, look at [substack's Twitter account](https://twitter.com/substack), or [/-/recent](http://studio.substack.net/-/recent).

The audio API is based on [baudio](https://www.npmjs.org/package/baudio), which works by accepting a function that takes a time value and returns an amplitude value between -1 and 1.

That means you can generate a sound just by running something like this:

{% highlight javascript %}
return function(t) {
  return sin(441);
  function sin(x) { return Math.sin(2 * Math.PI * t * x); }
}
{% endhighlight %}

That example creates a function called `sin` that generates values for a given pitch.  Code Studio will render an oscilloscope so you can visualise the output as well as hear it.  The waveform is rendered using [amplitude-viewer](https://www.npmjs.org/package/amplitude-viewer), another module by substack that creates graphs with SVG.

If you're interested in the server-side portion of the code, then take a look at [bin/cmd.js](https://github.com/substack/code-music-studio/blob/master/bin/cmd.js).  This uses Node's `http` module, and [ecstatic](https://www.npmjs.org/package/ecstatic) for static assets.

I think my favourite example so far is [polytropon](http://studio.substack.net/polytropon?time=1397235711071).  It has a function called `Moog`, so you can't go wrong!
