---
layout: post
title: "jQuery Roundup: Orangevolt Ampere, Succinct, jQuery Age"
author: Alex Young
categories:
- jquery
- plugins
- state-machine
- text
- time
- date
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="http://contact.dailyjs.com/project">contact form</a>.
</div>

###Orangevolt Ampere

![Orangevolt Ampere](/images/posts/orangevolt.png)

If you like state machines, then you might find [Orangevolt Ampere](http://lgersman.github.io/jquery.orangevolt-ampere/) (GitHub: [lgersman / jquery.orangevolt-ampere](https://github.com/lgersman/jquery.orangevolt-ampere), License: _MIT/GPL2_) interesting.  Created by Lars Gersmann, it uses AngularJS, jQuery, Boostrap, and Font Awesome and attempts to help you model single page applications by encapsulating data operations and route transitions in state machines.  That means your applications get some features for "free", like infinite undo/redo.

The author has made a [presentation about Orangevolt Ampere](http://lgersman.github.io/jquery.orangevolt-ampere/slides/) that gently introduces the main concepts, which I recommend looking at before diving into the code.

[The wizard example](http://ampere.eu01.aws.af.cm/public/examples/wizard/) is a good example of how state machines can model something that would ordinarily be awkward to work with.

###Succinct

[Succinct](http://micjamking.github.io/succinct/) (GitHub: [micjamking / succinct](https://github.com/micjamking/Succinct), License: _MIT_) by Mike King is a text truncation plugin.  It truncates based on the simplest case where you know the number of characters you want to display: `$('.truncate').succinct({ size: 80 })` will cut text down to 80 characters and add an ellipsis.

###jQuery Age

[jQuery Age](http://ksylvest.github.io/jquery-age/) (GitHub: [ksylvest / jquery-age](https://github.com/ksylvest/jquery-age)) by Kevin Sylvestre formats and tracks dates and times as human readable text.  It allows the text suffixes and grammatical formatting to be overridden, so it could be internationalised as needed.

{% highlight html %}
<time datetime="2010-01-01T12:00:00Z" class="age">January 1, 2010 12:00</time>
<time datetime="2020-01-01T12:00:00Z" class="age">January 1, 2020 12:00</time>

<script type="text/javascript">
  $('.age').age();
</script>
{% endhighlight %}
