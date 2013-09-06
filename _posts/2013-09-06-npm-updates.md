---
layout: post
title: "New Features in npm"
author: "Robert Kowalski"
categories: 
- node
- npm
---

npm is moving fast, so here are some features you might have missed since 1.3.7.

###Remove devDependencies

We've noticed people running into situations where `./node_modules` gathers cruft.  For example, installing `devDependencies` during deployment due to various reasons.

To clean up in npm 1.3.10 and above, just run: `npm prune --production`

###Repository Shorthands

Use the shorthand `"username/repo"` for the field repository in your `package.json`.

People generally use a full Git URL in the repository field:

{% highlight javascript %}
  "repository": {
    "type": "git",
    "url": "git@github.com:robertkowalski/npm-registry-mock.git"
  },
{% endhighlight %}

However, GitHub is the default, so you don't need to write the full URL.  This just got merged and is available in npm 1.3.10.  Here's an example:

{% highlight javascript %}
  "repository": {
    "type": "git",
    "url": "robertkowalski/npm-registry-mock"
  },
{% endhighlight %}

###Open Repositories Directly in a Browser

Since npm 1.3.8 the new command `npm repo` will open the repository website in your browser for the specified package.  For example, `npm repo express` will open the Express GitHub page.

### Conclusion

In npm 1.3.7 and up a huge amount of functionality has been added -- which is why you should always keep Node up to date!  I hope you learned something new about npm.  You can find me on Twitter [@robinson_k](http://twitter.com/robinson_k) and [GitHub at robertkowalski](http://github.com/robertkowalski).

