---
layout: post
title: "Introduction to On-Page Guidance"
author: "Oded Ben-David"
categories:
- on-screen guidance
- on-page guidance
- iridize
- tutorials
---

My name is Oded Ben-David, and I'm a co-founder at [Iridize](https://iridize.com/) -- a service for enhancing website user-experience through on-screen guidance.  Documentation is important to new users of a software product, yet it's typically added as an afterthought.  Worse, users don't always want to spend time reading documentation.  On-screen guidance turns this on its head by showing help where and when it's needed.

On-screen guidance is becoming more commonplace on the web. It is used by prominent companies including Facebook, Yahoo, and Google. Additionally, several JavaScript libraries for website on-screen guidance were published recently, most of which are mentioned below.

On-screen guidance seeks to solve two issues: presenting help __when__ and __where__ it is needed.  It should propel users to their goals and keep them focused on the task at hand, not stop them in their tracks and point their attention elsewhere, to external help texts and videos. Also, guidance should only be there when the user actually wants it. Permanently cluttering a web page with too much help will end up confusing users.

To actually implement this, on-screen guidance systems use an interactive layer over a web page that is activated either on-demand, or automatically based on business logic.

By guiding users step-by-step throughout fulfilling a task they are always focused on the task at hand. This provides first time users with an interactive site tour which helps illustrate key features.

These tools are not just for help content. Pointing out newly added or key but underused features can also benefit from being presented in a dedicated layer. This dedicated layer can also serve for increasing conversion, by inviting users to sign-up or subscribe, as well as increase user engagement by enticing them to try up a service or a feature.  It can easily be coupled with A/B testing services to further optimize conversions.

###Tutorial: Open Source On-Screen Guidance

There are several JavaScript libraries available for adding on-screen guidance to your project:

1. [king\_tour](http://salesking.github.com/king_tour/) is probably one of the earliest available libraries. Tours are defined as markup using a simple structure based around containers and `title` attributes. Global options and tour activation are handled by JavaScript.
2. [Joyride](http://www.zurb.com/playground/jquery-joyride-feature-tour-plugin) is a more modern jQuery plugin that takes a similar approach.
3. A different approach is taken by the very nice [bootstrap-tour](http://sorich87.github.com/bootstrap-tour/) (reviewed in [DailyJS](http://dailyjs.com/2012/07/06/bootstrap-tour-dom-utils-asevented/)), where steps are defined using a factory method, rather than in markup. Bootstrap-tours also manages a simple state and allows for some multi-page capabilities.
4. [Guiders.js](https://github.com/jeff-optimizely/Guiders-JS#readme) by the good people of Optimizley, is another library where guides can be automatically started using a special hash parameter, and an optional overlay can be used to highlight the element the guider refers to on the page.

Let's take a look at how to create a guide using the Guiders.js library. For the purpose of this short demonstration I have created a jsFiddle, where you can see the [final result](http://jsfiddle.net/nmScv/embedded/result/). The first thing we need for our demo is some page markup. I chose the markup for a bug-tracking form from the [free gallery](http://wufoo.com/gallery/) at [wufoo](http://wufoo.com/gallery/). Next, we need to embed jQuery, and the Guiders.js JavaScript and CSS files. jQuery is readily available via jsFiddle's default libraries. For this demo I am serving the Guiders.js sources from via our own CDN (so please do not hotlink there).

{% highlight html %}
<script type="text/javascript" src="https://static-iridize.netdna-ssl.com/static/guiders/guiders-1.2.8.js"></script>
<link rel="stylesheet" type="text/css" href="https://static-iridize.netdna-ssl.com/static/guiders/guiders-1.2.8.css">
{% endhighlight %}

Now that we are all set we can start adding guiders. For starters, let's add an introductory 'splash' tip with an overlay. Note that this bit of code should be executed on DOM ready event. This is the JavaScript for creating the first tip:

{% highlight javascript %}
guiders.createGuider({
  buttons: [{ name: 'Next' }]
, description: 'Introducing Guiders.js for the DailyJS readers. I am the first tip. Click my Next button to get started.'
, id: 'first'
, next: 'second'
, overlay: true
, title: 'Demoing Guiders.js!'
}).show();
{% endhighlight %}

There's quite a bit going on here, so I'll break it down. First, as mentioned before, guiders are created using the `createGuider` method, which accepts a configuration object containing the guider options. Guider ids are used for chaining them together using the `next` property. This guider is set as `first`, and the next guider will be the one with id `second`. Setting the overlay property to `true` tells sets an overlay mask blocking the rest of the page.

The `buttons` property sets which buttons should be displayed at the bottom of the tip. This property accepts an array of button definition objects. You can define custom buttons and custom button behaviors, but the three default buttons available are `Next`, `Close`, and `Prev`. For this first tip we set only a single `Next` button, used for going forward.

You may have noticed that there's another method call chained to the `createGuider` call, namely `.show()`.  Guiders are created hidden by default, so the `show()` method is called to show the first tip automatically. Of course, we could have saved a reference to the created guider in a variable instead, and issued the show call at a later time.

Now that the first guider is ready, a second can be added:

{% highlight javascript %}
guiders.createGuider({
  attachTo: '\#foli0'
, buttons: [{name: 'Close'}, {name: 'Next'}]
, description: 'Please write down the full URL of the page where you experienced a bug. You can copy paste it from the address bar.'
, id: 'second'
, next: 'third'
, position: 3
, title: 'Oh Where?'
});
{% endhighlight %}

This guider has two new properties: `attachTo` and `position`. The `attachTo` property accepts a selector for the element next to which the tip should be positioned. The `position` property specifies the position of the tip relative to the element specified by `attachTo`. The number stands for 'clock position', so specifying `3` makes the tip appear to the right of the element. This tip also has an option to close the guide, by adding the `Close` button to the buttons array. Also, note that `show()` was not called for this guider, as it should only be shown when clicking the `Next` button on the previous tip.

The rest of the tips in this short demo are more of the same. You can find the full reference of guider options on the [Guiders.js repository page](https://github.com/jeff-optimizely/Guiders-JS).

###Iridize

<iframe width="530" height="360" src="http://www.youtube.com/embed/ZyXD-A1ZClw?feature=player_detailpage" frameborder="0" allowfullscreen="allowfullscreen">
</iframe>

<p><em>Video showing one of the demos available at <a href="https://iridize.com/">iridize.com</a></em></p>

Our vision for Iridize was that the developer should not be required to create or maintain guidance material. Creating and embedding on-screen guidance should be at least as easy as creating a presentation. This should leave developers with more time to code instead of writing help guides.

Iridize is the realization of that vision - [on-page guidance and site-tours as a service](https://iridize.com/?stStart=welcome).

We created a fully visual editor which runs in the browser. This means that there is absolutely no installation required to get started. Other than embedding a generic JavaScript snippet there is no setup necessary even for deployment (similar to embedding Google Analytics). All JavaScript and guidance content is loaded from our servers, and delivered through a CDN -- with SSL if necessary.  Our service includes a full management system, complete with an editing and publishing cycle that supports collaboration for guide creation.

True to the spirit of providing guidance where and when it is needed, our guides can be launched by the end user from a side-panel or launched automatically based on the page path, parameters, or a hash URL fragment. We provide an API for even tighter control on how guides are started.

We are now in a close beta phase, and we would like to invite you to take a look and register for a [beta account](https://iridize.com/account/register/closed/). Moreover, as we are keen on giving back to the wonderful JavaScript community that built so many of the great tools we are using, we would like to offer free service to select open-source projects for the long term. Please [contact us](https://iridize.com/support/) if you are member of the core team of such a project that could benefit from our services (even if just for your public website).

###Conclusion

On-screen guidance can be a powerful tool for enhancing user-experience and improving website usability. Providing guidance where and when it is needed can alleviate the pains of first time and occasional website users, as well as expose new feature to the experienced crowd. Guiding users step-by-step keeps them focused and can ensure they don't miss or forget steps along the way.

Whether you choose to use [Iridize](https://iridize.com/?stStart=welcome) to implement on-screen guidance in your projects or decided to take the DIY route with one of the libraries I listed, we are certain that your users will thank you for helping them out!
