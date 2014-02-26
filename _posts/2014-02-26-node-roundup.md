---
layout: post
title: "Node Roundup: No More Force Publish, Counterpart, mock-fs"
author: Alex Young
categories:
- node
- modules
- npm
- testing
- internationalisation
---

###No More Force Publish

Isaac Z. Schlueter wrote on npm's blog that [publish -f will no longer work](http://blog.npmjs.org/post/77758351673/no-more-npm-publish-f):

> If you publish foo@1.2.3, you can still un-publish foo@1.2.3. But then, you will not be able to publish something else to that same package identifier and version.
> Ever.

The common wisdom is changing the code that a version number describes is dangerous, so it's better to publish a new version.  If you're a module author, you may feel that this is frustrating -- what if you just released something with a dangerous security flaw?  In cases like this it may be best to remove the version and publish a new, fixed version.

###Counterpart

Counterpart (GitHub: [martinandert / counterpart](https://github.com/martinandert/counterpart), License: _MIT_, npm: [counterpart](https://github.com/martinandert/counterpart)) by Martin Andert is an internationalisation module based on Ruby's [I18n gem](https://github.com/svenfuchs/i18n):

{% highlight javascript %}
translate('damals.about_x_hours_ago.one')          // => 'about one hour ago'
translate(['damals', 'about_x_hours_ago', 'one'])  // => 'about one hour ago'
translate(['damals', 'about_x_hours_ago.one'])     // => 'about one hour ago'
{% endhighlight %}

You can write translation documents using JSON.  Features include interpolation, pluralisation, and default fallbacks.

###mock-fs

mock-fs (GitHub: [tschaub / mock-fs](https://github.com/tschaub/mock-fs), License: _MIT_, npm: [mock-fs](https://www.npmjs.org/package/mock-fs)) by Tim Schaub is an API-compatible version of Node's `fs` module that essentially allows you to temporarily use an in-memory filesystem.

It provides a `mock` function that accepts a specification of the files you want to mock:

{% highlight javascript %}
mock({
  'path/to/fake/dir': {
    'some-file.txt': 'file content here',
    'empty-dir': {/** empty directory */}
  },
  'path/to/some.png': new Buffer([8, 6, 7, 5, 3, 0, 9]),
  'some/other/path': {/** another empty directory */}
});
{% endhighlight %}

You might find this useful if you want to write tests that avoid touching real files.
