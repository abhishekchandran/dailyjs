---
layout: post
title: "Do You Use the jQuery Plugin Site?"
author: Alex Young
categories:
- jquery
- plugins
---

The [jQuery Plugin Registry](http://blog.jquery.com/2013/01/16/announcing-the-jquery-plugin-registry/) was released in January 2013.  It uses its own JSON format for defining a plugin and requires that you add `http://plugins.jquery.com/postreceive-hook` as a [post-receive hook](https://help.github.com/articles/post-receive-hooks).  This lets the repository collect information about new and updated plugins.  The [plugin site's code](https://github.com/jquery/plugins.jquery.com) is open source, and the authors use GitHub to manage feature requests and bugs.

jQuery was released in 2006, and since then a lot has changed on the web.  In the JavaScript community there is a vocal group that has moved away from more monolithic frameworks, now that tools like npm, Bower, and Grunt have made it easier to manage dependencies and build client-side projects.  That doesn't mean jQuery isn't still influential, and it's still hugely popular.

What concerns me is despite jQuery's continued popularity, the number of new releases on [plugins.jquery.com](http://plugins.jquery.com/) is lacklustre.  It's far from stagnant, but [npm](https://npmjs.org/) leaves it in the dust.  Not a fair comparison?  Perhaps, but I know for a fact most of the plugins readers send DailyJS do not have `jquery.json` manifest files.  I find it increasingly common to see `package.json` or `bower.json` files.

Do you use the jQuery plugin site for publishing or discovering plugins?  If not, please discuss your issues with the service in the comments.  Also, if you've been writing client-side scripts without the jQuery dependency let us know your reasoning.
