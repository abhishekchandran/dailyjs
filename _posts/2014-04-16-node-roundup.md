---
layout: post
title: "Node Roundup: Do We Need peerDependencies, lazy-install, Time Require"
author: "Alex Young"
categories:
- node
- modules
- npm
- benchmarks
---

###Do We Need peerDependencies?

Isaac Schlueter [asked this question](https://twitter.com/izs/status/456211498503634944) on Twitter:

>Recently, peerDependencies has gotten more and more contentious. Srsly considering deprecation/removal.
> Thoughts?
> [github.com/npm/npm/issues/5080](https://github.com/npm/npm/issues/5080#issuecomment-40545599)

The discussion on Twitter and GitHub seems strongly for removing `peerDependencies`.  I agree with it simply because I hate explaining how it works.

Eran Hammer made an [interesting point](https://github.com/npm/npm/issues/5080#issuecomment-40556757) about the idea of a `compatibleWith` property:

> What we need is compatibleWith concept that simply warns you when you are using bad combinations. I think we can rename peerDeps and with some minor adjustment keep the functionality without annoying everyone. Making it a warning sign instead of a blocking feature would remove the "hell" part and those who chose to ignore warnings (as many already do with node versions) can continue to ignore.

###lazy-install

If that isn't enough npm craziness for you, then how about this?  lazy-install (GitHub: [adamrenklint / lazy-install](https://github.com/adamrenklint/lazy-install), License: _MIT_, npm: [lazy-install](https://www.npmjs.org/package/lazy-install)) by Adam Renklint can be used to install dependencies based on "group" names.

Let's say you wanted to specify dependencies for your production and test environments.  Your `package.json` could look like this:

{% highlight javascript %}
{
  "name": "myProject",
  "lazyDependencies": {
    "server": {
      "express": "4.0.0"
    },
    "test": {
      "mocha": "1.18.2"
    }
  }
}
{% endhighlight %}

Then in your code you can run `lazy.install` to trigger an `npm install` with the right options.  In fact, the module itself is basically a wrapper around `npm`.

###Time Require

![Time Require](/images/posts/timerequire.png)

How much time did that `require` take to require?  Now you can find out, with time-require! (GitHub: [jaguard / time-require](https://github.com/jaguard/time-require), License: _MIT_, npm: [time-require](https://www.npmjs.org/package/time-require)).

It shows the execution time for each module by changing `require`, and then displaying the elapsed time for each file once the `'exit'` event is emitted on the `process` object.

You can use it by adding a `require('time-require')` as the first line of your main script.
