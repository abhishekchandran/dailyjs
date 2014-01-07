---
layout: post
title: "Gulp, bLazy, grunt-bowercopy"
author: Alex Young
categories:
- bower
- grunt
- build
- images
- node
- modules
---

###Gulp

![Gulp](/images/posts/gulp.png)

Last night I was reading [a post about Gulp](http://www.100percentjs.com/just-like-grunt-gulp-browserify-now/) by Martin Genev.  Martin traces the appearance of Gulp into the JavaScript community, through GitHub comments and Tweets.

Apparently [Gulp](http://gulpjs.com/) is a new build system made by [Fractal](https://github.com/wearefractal), a Node consultancy with several popular Node modules under their collective belts.

Gulp is built around streams, so it feels more like idiomatic Node.  You can pipe files through processors, so if you had a set of LESS files you could convert them into CSS with something like `gulp.src('less/*.less').pipe(less()).pipe(minify()).pipe(gulp.dest('styles/screen.css'))`.  It supports tasks as a unit of work, and tasks can have names and dependencies.

The project has 13 contributors already -- most of the work is by [Eric Schoffstall](https://github.com/Contra) who you'll see all over Fractal's other projects.  It has tests written with Mocha, and some decent documentation already.

###bLazy

[bLazy](http://dinbror.dk/blazy/) (GitHub: [dinbror / blazy](https://github.com/dinbror/blazy/)) by Bjoern Klinggaard is a lazy loading image script.  It doesn't have any dependencies, and supports callbacks for loading failures:

{% highlight javascript %}
var bLazy = new Blazy({
  success: function(ele) {
  },
  error: function(ele, msg) {
    if (msg === 'missing') {
      // Data-src is missing
    } else if (msg === 'invalid') {
      // Data-src is invalid
    }
  }
});
{% endhighlight %}

There's a [blog post about bLazy](http://dinbror.dk/blog/blazy/) that documents the full API.

###grunt-bowercopy

I seem to waste a lot of time detangling Bower dependencies to make my client-side builds more efficient.  Timmy Willison may have solved this with grunt-bowercopy (GitHub: [timmywil / grunt-bowercopy](https://github.com/timmywil/grunt-bowercopy), License: _MIT_).  It allows you to specify where dependencies should go, and can reduce the amount of duplication when creating builds.

It looks like it works the way I expect Bower dependency management to work in Grunt, so I'm going to go back and look at my Grunt/Bower projects to see if I can clean then up with this.
