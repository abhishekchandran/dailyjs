---
layout: post
title: "Static Site Generators for Yeoman"
author: "The Angry JavaScript Nerd"
categories:
- node
- modules
- yeoman
- rants
---

I often find myself being the only guy in the team who can make (or wants to make) a good ol' fashioned website.  No dynamic stuff, just a simple static marketing site to sell a product.  "No problem," I say confidently, dreaming up designs I can implement rapidly with Vim, Bootstrap, and [Glyphish](http://www.glyphish.com/).

The problem I've ran into consistently over the last year or so is Yeoman doesn't do what I think it does.  This is what it does in my head:

* Unites Grunt, Bower
* Runs a little web server so I can see my site without having to run a web server
* Doesn't install any Ruby nonsense
* Uses idiomatic Node

Here's what it actually does when I use `generator-webapp`:

* Installs loads of weird stuff I don't need to do with testing and image optimisation
* Make a `Gruntfile.js` that isn't formatted using the coding style of most community Node projects
* Seems to need Ruby due to Sass when I make it install Bootstrap

Then I realise `generator-webapp` might not be for me, so I try starting a project from scratch.  Then I get into an incredible mess trying to automate the minimization of each Bower component's JavaScript, CSS, and copying assets to a suitable location with Grunt.

###I Miss Makefiles

Here's how you copy a file in the shell:

{% highlight text %}
* cp tmp/*/*.min.js site/js/
{% endhighlight %}

Here's how you do it with Grunt:

{% highlight javascript %}
copy: {
  dist: {
    files: [{
      expand: true,
      cwd: 'tmp/',
      src: ['*.min.js'],
      dest: 'site/js/',
      filter: 'isFile'
    },
{% endhighlight %}

Not only is it a whole bunch of lines to do something that should be simple, it also has weirdly named properties.  I see `isFile` and start an internal monologue about everything being a file because it's Unix.

I could write a `Makefile` in two lines that does this.

###Yeoman Static Site Generators

This time I decided to persevere: I tried a bunch of static site generators for Yeoman.

* [Armadillo](https://github.com/Snugug/generator-armadillo): Installed lots of stuff I didn't need, and needed Ruby
* [Go Static](https://github.com/colynb/generator-go-static): Was more for blogs than simple sites, and seemed to make files indented with tabs

There were more but I only have bad things to say about them.  What I ended up with was this:

* `grunt-contrib-connect` for running a web server.  It was more complex than it needed to be because it defaults to exiting automatically rather than running a server, you need to specify a `keepalive` setting
* `grunt-contrib-concat` for concatenating Bootstrap's CSS, JavaScript, and any other dependencies in `bower_components`
* `grunt-contrib-copy` for copying the files from `bower_components` to my website's asset directories

###The Shit Sandwich

I think the reason I have difficulty with Yeoman and Grunt is I see client-side development as "open source stuff" and "my stuff".  I want open source stuff poured out into buckets that I never look at, in a way that's easy for other people to repeat should they want to install the dependencies fresh (I keep the files in the repository), or experiment with upgraded versions of each module.

Conversely, _my stuff_ should be elegantly encapsulated with a module loader like RequireJS, kept separate and decoupled.

Instead of a neatly organized bento box with very clear sections I end up with a shit sandwich.
