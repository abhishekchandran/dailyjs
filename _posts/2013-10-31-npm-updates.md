---
layout: post
title: "New Features in npm: Part 2"
author: "Robert Kowalski"
categories: 
- node
- npm
---

<div class="intro">
Node has one of the best package managers around: npm. Every month a lot of features are added to npm.  Here are some new features as of 1.3.12.
</div>

###Default Homepage URLs

Many projects use the same URL for their homepage and GitHub page.  As of 1.3.12, you do not have to define the `homepage` property in your `package.json` -- if you have a GitHub URL as the `repository` field the homepage will default to the GitHub page.

For example, this:

{% highlight javascript %}
"repository": {
  "type": "git",
  "url": "git@github.com:robertkowalski/npm-registry-mock.git"
},
{% endhighlight %}

will result in the `homepage` field being set to <http://github.com/robertkowalski/npm-registry-mock>.

###Outdated Upate

`npm outdated` shows the latest compatible version of each module according to your `package.json` definition. The updated version of this command, which you can use with npm 1.3.12, will also show the very latest version, even if it is not compatible with your `package.json` definitions.

These will show as `latest`:

{% highlight text %}
underscore node_modules/underscore current=1.3.1 wanted=1.3.3 latest=1.5.1
{% endhighlight %}

###Conclusion

With a new version of npm (and also Node) a ton of features and bug fixes arrive, so you should always be up to date. Fortunately, you just have to to get the latest Node version each time, as the latest npm versions are bundled into each node release.

You can find me on Twitter [@robinson_k](https://twitter.com/robinson_k) and GitHub at [robertkowalski](https://github.com/robertkowalski).
