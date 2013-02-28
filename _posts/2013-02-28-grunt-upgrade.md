---
layout: post
title: "Upgrading to Grunt 0.4"
author: Alex Young
categories: 
- backbone.js
- node
- backgoog
---

I was working on [dailyjs-backbone-tutorial](https://github.com/alexyoung/dailyjs-backbone-tutorial) and I noticed [issue #5](https://github.com/alexyoung/dailyjs-backbone-tutorial/issues/5) where "fiture" was unable to run the build script.  That tutorial uses [Grunt](http://gruntjs.com/) to invoke `r.j` from RequireJS, and it turned out I forgot to specify the version of Grunt in the project's `package.json` file, which meant newcomers were getting an incompatible version of Grunt.

I changed the project to first specify the version of Grunt, and then renamed the grunt file to `Gruntfile.js`, and it pretty much worked.  You can see these changes in [commit 0f98f7](https://github.com/alexyoung/dailyjs-backbone-tutorial/commit/0f98f7053bf4a7d58be278ed7319b9758dd7ff05).

So, what's the big deal?  Why is Grunt breaking projects and how can this be avoided in the future?

###Global vs. Local

If you're a client-side developer, npm is probably just part of your toolkit and you don't really care about how it works.  It gets things like Grunt for you so you can work more efficiently.  However, us server-side developers like to obsess about things like dependency management, and to us it's important to be careful about specifying the version of a given module.

Previous versions of Grunt kind of broke this whole idea, because Grunt's documentation assumed you wanted to install Grunt "globally".  I've never liked doing that, as I've experienced why this is bad first-hand with the Ruby side projects I've been involved with.  What I've always preferred to do with Node is write a `package.json` for every project, and specify the version of each dependency.  I either specify the exact version, or the minor version if the project uses [semantic versioning](http://semver.org/).

For example, with Grunt I might write this:

{% highlight javascript %}
 , "grunt": "0.3.x"
{% endhighlight %}

This causes the `grunt` command-line tool to appear in `./node_modules/.bin/grunt`, which probably isn't in your `$PATH`.  Therefore, when you're ready to build the project and you type `grunt`, the command won't be found.

Knowing this, I usually add `node_modules/.bin/grunt` as a "script" to `package.json` which allows `grunt` to be invoked through the `npm` command.  This works in Unix and Windows, which was partly the reason I used Grunt instead of `make` anyway.

There were problems with this approach, however.  Grunt comes with a load of built-in tasks, so when the developers updated one of these smaller sub-modules they had to release a whole new version of Grunt.  This is dangerous when a module is installed globally -- what happens if an updated task has an API breaking change?  Now _all_ of your projects that use it need to be updated.

To fix this, the Grunt developers have pulled out the command-line part of Grunt from the base package, and they've also removed the tasks and released those as plugins.  That means you can now write this:

{% highlight javascript %}
 , "grunt": "0.4.x"
{% endhighlight %}

And install the command-line tool globally:

{% highlight text %}
npm install -g grunt-cli
{% endhighlight %}

Since `grunt-cli` is a very simple module it's safer to install it globally, while the part that we want to manage more carefully is locked down to a version range that shouldn't break our project.

###Built-in Tasks: Gone

The built-in tasks have been removed in Grunt 0.4.  I prefer this approach because Grunt was getting extremely large, so it seems natural to move them out into plugins.  You'll need to add them back as `devDependencies` to your `package.json` file.

If you're having trouble finding the old plugins, they've been flagged on the [Grunt plugin site](http://gruntjs.com/plugins) with stars.

###Uninstall Grunt

Before switching to the latest version of Grunt, be sure to uninstall the old one if you installed it globally.

###Other Changes

There are other changes in 0.4 that you may run into that didn't affect my little Backbone project.  Fortunately, the Grunt developers have written up [a migration guide](http://gruntjs.com/upgrading-from-0.3-to-0.4) which explains everything in detail.

Also worth reading is [Tearing Grunt Apart](http://weblog.bocoup.com/tearing-grunt-apart/) in which Tyler Kellen and Ben Alman explain why Grunt has been changed, and what to look forward to in 0.5.

###Peer Dependencies

If you write Grunt plugins, then I recommend reading [Peer Dependencies](http://blog.nodejs.org/2013/02/07/peer-dependencies/) on the Node blog by Domenic Denicola.  As a plugin author, you can now take advantage of the `peerDependencies` property in `package.json` for defining the version of Grunt that your plugin is compatible with.

Take a look at [grunt-contrib-requirejs/package.json](https://github.com/gruntjs/grunt-contrib-requirejs/blob/master/package.json) to see how this is used in practice.  The authors have locked the plugin to Grunt 0.4.x.

