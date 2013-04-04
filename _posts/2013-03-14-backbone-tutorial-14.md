---
layout: post
title: "Backbone.js Tutorial: Customising the UI"
author: Alex Young
categories: 
- backbone.js
- mvc
- node
- backgoog
- bootstrap
---

<ul class="parts">
  <li><a href="http://dailyjs.com/2012/11/29/backbone-tutorial-1/">Part 1: Build Environment</a></li>
  <li><a href="http://dailyjs.com/2012/12/06/backbone-tutorial-2/">Part 2: Google's APIs and RequireJS</a></li>
  <li><a href="http://dailyjs.com/2012/12/13/backbone-tutorial-3/">Part 3: Authenticating with OAuth2</a></li>
  <li><a href="http://dailyjs.com/2012/12/20/backbone-tutorial-4/">Part 4: Backbone.sync</a></li>
  <li><a href="http://dailyjs.com/2012/12/27/backbone-tutorial-5/">Part 5: List Views</a></li>
  <li><a href="http://dailyjs.com/2013/01/03/backbone-tutorial-6/">Part 6: Creating Lists</a></li>
  <li><a href="http://dailyjs.com/2013/01/10/backbone-tutorial-7/">Part 7: Editing Lists</a></li>
  <li><a href="http://dailyjs.com/2013/01/17/backbone-tutorial-8/">Part 8: Deleting Lists</a></li>
  <li><a href="http://dailyjs.com/2013/01/24/backbone-tutorial-9/">Part 9: Tasks</a></li>
  <li><a href="http://dailyjs.com/2013/01/31/backbone-tutorial-10/">Part 10: Oh No Not More Tasks</a></li>
  <li><a href="http://dailyjs.com/2013/02/07/backbone-tutorial-11/">Part 11: Spies, Stubs, and Mocks</a></li>
  <li><a href="http://dailyjs.com/2013/02/14/backbone-tutorial-12/">Part 12: Testing with Mocks</a></li>
  <li><a href="http://dailyjs.com/2013/03/07/backbone-tutorial-13/">Part 13: Routes</a></li>
  <li><a href="http://dailyjs.com/2013/03/14/backbone-tutorial-14/"><strong>Part 14: Customising the UI</strong></a></li>
  <li><a href="http://dailyjs.com/2013/03/28/backbone-tutorial-15/">Part 15: Updates for 1.0, Clear Complete</a></li>
  <li><a href="http://dailyjs.com/2013/04/04/backbone-tutorial-16/">Part 16: jQuery Plugins</a></li>
</ul>

###Preparation

Before starting this tutorial, you'll need the following:

* [alexyoung / dailyjs-backbone-tutorial](https://github.com/alexyoung/dailyjs-backbone-tutorial) at commit `85c358`
* The API key from part 2
* The "Client ID" key from part 2
* Update `app/js/config.js` with your keys (if you've checked out my source)

To check out the source, run the following commands (or use a suitable Git GUI tool):

{% highlight text %}
git clone git@github.com:alexyoung/dailyjs-backbone-tutorial.git
cd dailyjs-backbone-tutorial
git reset --hard 85c358
{% endhighlight %}

###Customising Bootstrap

<div class="image">
  <img src="/images/posts/backbone-app-before.png" alt="" />
  <small>Before customisation.</small>
</div>

So far our Backbone application has had a rudimentary interface.  It's based on [Bootstrap](http://twitter.github.com/bootstrap/), which is a popular choice for developers who want a usable interface without spending too much time working on the design side of things.  However, Bootstrap is a victim of its own popularity, and most of us are starting to grow tired of seeing it everywhere.

This post is about techniques for customising projects built with Backbone and Bootstrap.  There are three main approaches I use to add some originality to my Bootstrap projects:

1. Colours: Get the project configured with suitable branding
2. Texture: Judicious use of images to add an extra dimension to background, panels, and buttons
3. Custom fonts and icons: Carefully applied custom fonts and icons can create a more distinct look

###Colours

[Bootstrap has a customisation page](http://twitter.github.com/bootstrap/customize.html) that allows you to change typographic elements and colours.  This is self-explanatory so I'm not going to spend too much time on it.  Bootstrap is built on [LESS CSS](http://lesscss.org/) so it's easy to create your own builds of Bootstrap with custom colours baked right in.

###Texture

<div class="image">
  <img src="/images/posts/subtlepatterns.png" alt="" />
  <small>Subtle Patterns.</small>
</div>

To save time when working on client projects, I'll often dig through stock photography sites to find useful illustrations and textures.  This project, however, just needs something to add a texture to the left-hand-side navigation to make it look visually distinct.  An excellent resource for textures is [Subtle Patterns](http://subtlepatterns.com/) -- a curated directory of tiled textures suitable for web and mobile projects.  For legal information for use in commercial projects, see [About Subtle Patterns](http://subtlepatterns.com/about/).

I've added two tiled images to the project: one for the navigation bar and another for the `body` background.  The image used on the `body` is white, while the navigation bar is dark grey.  The navigation list elements use alpha blending to make the underlying texture appear lighter, with `rgba(255, 255, 255, .25)`.

It's easy to add textures to a project, particularly when they tile, and the Subtle Patterns images include a higher-DPI version as well.  I find this a fun second stage to Bootstrap customisation, because it's easy to quickly swap textures around to experiment.

###Custom Fonts and Icons

<div class="image">
  <img src="/images/posts/btask-custom-font.png" alt="" />
  <small>Using Google Web Fonts.</small>
</div>

The first thing I wanted to change was the logo font.  Rather than using an image I found a suitable font on [Google Web Fonts](http://www.google.com/webfonts) and applied some CSS shadows.  This font was added to the project by updating `index.html` to load the font and updating the CSS to refer to it by name:

{% highlight html %}
<link href='http://fonts.googleapis.com/css?family=Playball' rel='stylesheet' type='text/css'>
{% endhighlight %}

Then in the CSS the font is selected with `font-family: playball, sans-serif`.

I also switched the main `body` font to `PT Sans`, which doesn't look radically different to the default but again elevates the look and feel away from stock-Bootstrap.

Another quick win is to use [Font Awesome](http://fortawesome.github.com/Font-Awesome/).

###Go Forth and Customise

<div class="image">
  <img src="/images/posts/bootstrap-customised.png" alt="" />
  <small>The finished article.</small>
</div>

Adding custom fonts, textures, and icons are just a few easy ways to distinguish a Bootstrap-based project from the crowd.  You've got no excuse for releasing boring-looking apps!

I'm running a build of bTask at [todo.dailyjs.com](http://todo.dailyjs.com/).  It's not exactly the same as the tutorial version at the moment because I wrote it while researching this tutorial series, but eventually I'll switch it over to use the same code as the GitHub project.  It doesn't implement everything Google Tasks supports (like subtasks for example), but I use it every day at work.

The full source for this tutorial can be found in [alexyoung / dailyjs-backbone-tutorial, commit 711c9f6](https://github.com/alexyoung/dailyjs-backbone-tutorial/commit/711c9f6c1df36187417b18fba84a44fe82889695).

