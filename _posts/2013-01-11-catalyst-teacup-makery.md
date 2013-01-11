---
layout: post
title: "Catalyst, Teacup, Makery"
author: Alex Young
categories:
- sponsored-content
- testing
- templates
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###Catalyst

<div class="sponsored-content" style="background-color: #f0f4cf; padding: 0; margin: 10px 0; border-radius: 5px; font-size: 90%; width: 530px; padding: 0 1px">
  <p><a class="label" href="/sponsored-content.html">Sponsored Content</a> This post is about a commercial product that we think will appeal to DailyJS readers.</p>
</div>

![Catalyst](/images/posts/catalyst.png)

Learning JavaScript?  Join [Catalyst](http://catalystclass.com)!  Full-time, in-person training and job placement services over 12 weeks in San Francisco.  Instructors and speakers from Twitter, OkCupid, Adobe, Meteor, and more.

For more information, visit [catalystclass.com](http://catalystclass.com).

###Teacup

[Teacup](http://goodeggs.github.com/teacup/) (GitHub: [goodeggs / teacup](https://github.com/goodeggs/teacup), License: _MIT_, npm: [teacup](https://npmjs.org/package/teacup)) by Good Eggs is a CoffeeScript templating language.  It comes with middleware that can be used alongside [connect-assets](https://github.com/TrevorBurnham/connect-assets) for compiling the templates, and the language kind of reminds me of CoffeeScript crossed with Jade:

{% highlight coffeescript %}
{renderable, js, css, html, head, body} = require 'teacup'

module.exports = renderable ->
  html ->
    head ->
      js 'app'
      css 'app'
    body ->
      # ...
{% endhighlight %}

It works in browsers, has Mocha tests, and also has a gem for Rails: [Teacup::Rails](https://github.com/goodeggs/teacup-rails).  The author wrote a blog post about it here: [Teacup: CoffeeScript Templates for Developer Happiness](http://bytes.goodeggs.com/post/40042760798/teacup-coffeescript-templates-for-developer-happiness).

###Makery

[Makery](https://github.com/leoasis/makery.js) (License: _MIT_, npm: [makery](https://npmjs.org/package/makery)) by Leonardo Garcia Crespo is a module for making objects to aid with testing --  the author says it works well for testing Backbone models.  The API looks like this:

{% highlight javascript %}
Makery.blueprint(MyConstructor, function() {
  return {
    id: this.unique(),
    aProperty: 'Some value',
    anotherProperty: 'Another value'
  };
});

var obj = MyConstructor.make();
{% endhighlight %}

Jasmine tests have been included, and it can be used in browsers as long as Underscore is present.

