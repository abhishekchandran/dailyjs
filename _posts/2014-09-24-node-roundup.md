---
layout: post
title: "Node Roundup: npm 2.0, nvm for Windows, xtpl"
author: "Alex Young"
categories:
- modules
- libraries
- node
- npm
- windows
- templating
---

###npm 2.0

[npm 2.0](http://blog.npmjs.org/post/98131109725/npm-2-0-0) has been released, and the announcement post has lots of details on the fixes it includes and the project's evolving release process.  One major change is `run-script` now accepts arguments:

> In `npm@2.0.0`, Ben changed `npm run-script` to allow you to pass arguments into scripts. That's a breaking change. It's as simple as that. Think of npm 2 as a step on the road towards getting npm right with semver. (There will be more. npm 3 will be out before the end of the year.)

The npm blog also has a post about [multi-stage installs](http://blog.npmjs.org/post/98233700815/multi-stage-installs-and-a-better-npm):

> Multi-stage installs will touch and improve all of the actions npm takes relating to dependencies and mutating your node_modules directory. This affects install, uninstall, dedupe, shrinkwrap and, obviously, dependencies (including optionalDependencies, peerDependencies, bundledDependencies and devDependencies).

This post mentions that npm should be getting progress bars soon, and changes that bring it closer to supporting transactional installation.

###nvm for Windows

Apparently, most Node version managers for Windows use batch files, so Corey Butler decided to try a different approach:

> This version of nvm has no dependency on node. It's written in Go, which is a much more structured approach than hacking around a limited .bat file. It does not rely on having an existing node installation. Plus, should the need arise, Go offers potential for creating a Mac/Linux version on the same code base with a substantially easier migration path than converting a bunch of batch to shell logic.

You can get the source from GitHub at [coreybutler / nvm](https://github.com/coreybutler/nvm), and he's got [binary releases as well](https://github.com/coreybutler/nvm/releases).

Corey also sent something called [Fenix Web Server](http://fenixwebserver.com/) (GitHub: [coreybutler / fenix](https://github.com/coreybutler/fenix), License: _GPL_), which is a static desktop web server powered by node-webkit:

> You can quickly fire up/kill web servers through a GUI or the command line. It has push-button sharing capabilities (localtunnel). There's also a visual webhook receiver for viewing incoming requests, which also leverages localtunnel.

I like the idea of being able to easily create a static server and then share content with a tunnel.

###xtpl

Yiming He sent in xtpl (GitHub: [kissyteam / xtpl](https://github.com/kissyteam/xtpl), License: _MIT_, npm: [xtpl](https://www.npmjs.org/package/xtpl)), an Express/Koa wrapper for [eXtensible Template Engine](https://github.com/kissyteam/xtemplate).  This template language is similar to others like ejs, but also allows you to add your own synchronous or asynchronous commands.

You can actually add commands to the template language, and they can be inline, block, and asynchronous.  Here's an example:

{% highlight javascript %}
XTemplate.addCommand('xInline', function(scope, option, buffer) {
  buffer = buffer.async(function(newBuffer) {
    setTimeout(function() {
      newBuffer.write(option.params[0] + 1).end();
    },10);
  });

  return buffer;
});
{% endhighlight %}

[The API documentation](https://github.com/kissyteam/xtemplate/blob/master/docs/api.md) has more examples, and xtpl's readme has some Koa samples as well.

