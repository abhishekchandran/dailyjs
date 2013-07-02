---
layout: post
title: "jQuery Roundup: minimit-anima, loda-button"
author: Alex Young
categories:
- jquery
- plugins
- icons
- animations
- css3
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="http://contact.dailyjs.com/project">contact form</a>.
</div>

###minimit-anima

![/images/posts/minimit.png](minimit-anima)

[minimit-anima](http://www.minimit.com/projects/code/minimit-anima-plugin) (GitHub: [minimit / minimit-anima](https://github.com/minimit/minimit-anima), License: _MIT_, jQuery: [minimit-anima](http://plugins.jquery.com/minimit-anima/)) by Riccardo Caroli is an animation plugin that uses hardware accelerated CSS3 animations with fallbacks for older browsers.  The API is queue-based like jQuery's standard animation API.  The following example specified an `easeOut` of 400ms:

{% highlight javascript %}
$(this).anima({ x: 20, y: 20 }, 400);
{% endhighlight %}

Hardware acceleration can be triggered by adding the `z` co-ordinate and `perspective` properties:

{% highlight javascript %}
$(this).anima({ x: 200, z: 0, perspective: 1000 }, 800);
{% endhighlight %}

The API has other features, like delaying animations with `delayAnima(ms)`, clearing the queue with `clearAnima`, and stopping the current animation with `stopAnima`.  Any CSS property can be animated, along with shortcuts for `scale[X|Y|Z]`, `rotate`, and `skew`.
###loda-button

![loda-button](/images/posts/lodabutton.png)

[loda-button](http://lugolabs.com/blog/2013/06/23/loda-button) (GitHub: [lugolabs / loda-button](https://github.com/lugolabs/loda-button)) by Artan is a small plugin that animates the icon in a button while an asynchronous operation is performed.  The recommended markup uses anchors and spans:

{% highlight html %}
<a href="#" class="loda-btn">
  <span aria-hidden="true" class="loda-icon icon-mail"></span>
  Mail
</a>
{% endhighlight %}

And requires a bit of JavaScript to set it up:

{% highlight javascript %}
var lodaBtn = $('#loda-btn').lodaButton();
{% endhighlight %}

The animation can be triggered by passing `start` to the button:

{% highlight javascript %}
lodaBtn.lodaButton('start');
{% endhighlight %}

The icon fonts are [IcoMoon by Keyamoon](http://icomoon.io/app/).

