---
layout: post
title: "Choosing an MVC Framework, lrNotifier"
author: Alex Young
categories:
- mvc
- angularjs
---

###Choosing a JavaScript MVC Framework

Deciding on a client-side MVC framework can be tough -- you don't want to invest too much time on something that isn't the right fit for your project.  Craig McKeachie sent in his article, [Choosing a JavaScript MVC Framework](http://www.funnyant.com/choosing-javascript-mvc-framework/), which reviews the most popular libraries like AngularJS and Backbone.js.  He takes into account things like the community following, maturity, and code size:

> How many real-world production apps are using these frameworks and how many users do these apps have?  How good is the documentation and how many examples/tutorials are available?  Are the examples up to date?  How stable is the API?  Do other developers know or are getting to know this technology?

He notes that these frameworks actually fall into subcategories, so it's hard to directly compare each of them.

> After looking at the projects by features it became clear to me that I wasn't really comparing "apples to apples."  A more fair comparison might be to compare full frameworks like AngularJS and EmberJS with stacks that include great but less broad libraries like Backbone and KnockoutJS.

The article also introduces the main concepts used by these libraries, so if you're confused about data binding or models then this should get you started.

###lrNotifier

[lrNotifier](http://lorenzofox3.github.io/lr-notifier/) (GitHub: [lorenzofox3 / lr-notifier](https://github.com/lorenzofox3/lr-notifier), License: _MIT_) by Laurent Renard is an AngularJS directive for showing notifications.  Notifications can be split into channels, allowing you to control where info, debug, or error messages will be displayed.

{% highlight javascript %}
app.controller('myCtrl', ['lrNotifier', function(notifier) {
  var channel=notifier('channelName');

  channel.pushNotification({ message: 'hello channel', otherProp: 'other' });
  channel.info('a great message');
  channel.warn('a great message');
  channel.error('a great message');
}]);
{% endhighlight %}
