---
layout: post
title: "Node Roundup: CampJS, bower-registry, Helmsman"
author: "Alex Young"
categories: 
- node
- modules
- events
- command-line
- bower
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a>.
</div>

###CampJS

![CampJS August](/images/posts/campjsaug.png)

[CampJS](http://campjs.com/) will be held in the Gold Coast, Australia, on August 9th to 12th.  [TJ Holowaychuk will be attending](http://campjs.com/#campjs-tj-holowaychuk), and also [Angelina Fabbro](http://campjs.com/#campjs-angelina-fabbro).

If you're interested, [tickets start at AU$320](http://tickets.campjs.com/).  DailyJS readers can get a $25 discount by using the code `DAILYJS`.

###bower-registry

If you're looking to set up your own [Bower](http://bower.io/) registry, then take a look at bower-registry (GitHub: [neoziro / bower-registry](https://github.com/neoziro/bower-registry), License: _MIT_, npm: [bower-registry](https://npmjs.org/package/bower-registry)) by Greg Bergé.  This is an Express web application that stores data in Redis, but the author notes it could be easily adapted to support other databases like MongoDB and PostgreSQL.

Running `bower-registry -d redis` on the command-line will start a server.  Other options can be viewed by typing `bower-registry -h`.  The app can also be loaded as a Node module, and `require('bower-registry').Registry` is the Express app instance.

###Helmsman

Helmsman (GitHub: [mattmcmanus / node-helmsman](https://github.com/mattmcmanus/node-helmsman), License: _MIT_, npm: [helmsman](https://npmjs.org/package/helmsman)) by Matt McManus is an opinionated command-line application development kit.  The interface style is based on Git's subcommands:

> A common setup for command line applications is `<command> <subcommand> <arguments/options>` (for example: `git commit -m 'message'`). Rather than having a giant file that `switch`es or `if else`s over each potential subcommand, it's much neater to store each subcommand in it's own file (`bin/command`,`bin/command-subcomand`, `bin/command-subcommand2`, etc). Doing this however introduces some annoying manual steps which `helmsman` hopes to solve.

The subcommand-style API is based on metadata exposed through `exports`.  If the file is run directly rather than loaded with `require`, then your script should run as it would normally:

{% highlight javascript %}
#!/usr/bin/env node

// 1. To expose the metadata simply `exports.command`
exports.command = {
  description: 'Show current worker counts and their pids'
};

// 2. Then make sure it only runs when it's directly called:
if (require.main === module) {
  // Parse options and run the magic
}
{% endhighlight %}
