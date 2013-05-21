---
layout: post
title: "jQuery Roundup: 1.10, jquery-markup, zelect"
author: Alex Young
categories:
- jquery
- plugins
- markup
- templating
- select
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="/contact.html">contact form</a>.
</div>

###jQuery 1.10

A new 1.x branch of jQuery has been released, [jQuery 1.10](http://blog.jquery.com/2013/05/09/jquery-1-10-beta-1-released/).  This builds on the work in the 1.9 line:

> It's our goal to keep the 1.x and 2.x lines in sync functionally so that 1.10 and 2.0 are equal, followed by 1.11 and 2.1, then 1.12 and 2.2...

A few of the inclded fixes were things originally planned for 1.9.x, and others are new to this branch.  As always the announcement blog post contains links to full details of each change.

###jquery-markup

[jquery-markup](http://plugins.jquery.com/markup/) (GitHub: [rse / jquery-markup](https://github.com/rse/jquery-markup), License: _MIT_) by Ralf S. Engelschall is a markup generator that works with several template engines (including Jade and handlebars).  By adding a tag, `<markup>`, `$(selector).markup` can be used render templates interpolated with values.

Ralf said this about the plugin:

> I wanted to use template languages like Handlebars but instead of having to store each fragment into its own file I still wanted to assemble all fragments together. Even more: I wanted to logically group and nest them to still understood the view markup code as a whole.

The `<markup>` tag can include a `type` attribute that is used to determine the templating language -- this means you can use multiple template languages in the same document.

###zelect

[zelect](http://mtkopone.github.io/zelect/) (GitHub: [mtkopone / zelect](https://github.com/mtkopone/zelect), License: _WTFPL_) by Mikko Koponen is a `<select>` component.  It's unit tested, and has built-in support for asynchronous pagination.

Unlike Chosen, it doesn't come with any CSS, but that might be a good thing because it keeps the project simple.  Mikko has provided an example with suitable CSS that you can use to get started.

If Chosen seems too large or inflexible for your project, then zelect might be a better choice.
