---
layout: post
title: "txtjs, Useuses"
author: "Alex Young"
image: "/images/posts/txtjs-small.png"
categories:
- text
- typesetting
---

###txtjs

Ted Patrick sent in [txtjs](http://txtjs.com/) (GitHub: [diverted247/txtjs](https://github.com/diverted247/txtjs), License: _BSD_), a typesetting engine.  It provides font and glyph rendering that is indepenent of the OS and browser by using SVGPath on a `canvas` element.

The documentation has lots of examples so you can see how it handles things like character styling with multiple fonts and alignment.  The project comes with a warning that says txtjs should be used for "creative applications" where the layout requirements exceed the capabilities of the DOM.  I imagine it could be useful in a scenario where tight control is required for graphic design projects.

txtjs is part of [CreateJS](http://www.createjs.com/#!/CreateJS), an open source set of libraries including [EaselJS](http://www.createjs.com/#!/EaselJS) and [TweenJS](http://www.createjs.com/#!/TweenJS).

###Useuses

[Useuses](http://spoonx.github.io/useuses/) (GitHub: [SpoonX/useuses](https://github.com/SpoonX/useuses), License: _BSD-2-Clause_, npm: [useuses](https://www.npmjs.org/package/useuses)) by Wesley Overdijk is a library for handling "soft" dependencies.  Given a JavaScript file, you can express the dependencies with `@uses ./my-dependency.js` in a comment.

Once you've defined dependencies you can create builds with the command-line tool, like this:

{% highlight text %}
useuses -i example/main.js -o example/dist/built.js -w
{% endhighlight %}

There's also a Node API, so you could hook it into a Grunt or Gulp.  Wesley had created an earlier version that was for Grunt, but this is a rewritten, more generic version.  He's written a blog post about [JavaScript dependency management](http://blog.spoonx.nl/javascript-dependency-management/) that describes the module in more details.
