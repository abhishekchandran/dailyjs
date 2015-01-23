---
layout: post
title: "EvenNode, Mozaik, Marko"
author: Alex Young
image: "/images/posts/evennode.png"
categories:
- node
- modules
- libraries
- sponsored-content
- hosting
---

### EvenNode

<div class="sponsored-content">
  <p><a class="label" href="/sponsored-content.html">Sponsored Content</a> This post is about a commercial product that we think will appeal to DailyJS readers.</p>
</div>

[EvenNode](http://www.evennode.com/?utm_source=dailyjs&utm_medium=cpc&utm_campaign=promo) is a new hosting service that is dedicated to Node.js.  You can get a free app instance which even includes MongoDB, so it's great for quickly deploying MEAN apps.  The [paid tiers](http://www.evennode.com/pricing?utm_source=dailyjs&utm_medium=cpc&utm_campaign=promo) start at &euro;6, which gets you 1GB storage and 256MB RAM.  One interesting thing about the paid tiers is they all get unlimited custom domain names, so it's easy to use multiple domain names for each application.

![EvenNode](/images/posts/evennode.png)

EvenNode supports multiple versions of Node, starting at 0.8.6.  You can deploy with Git, and WebSockets are supported out of the box.  For more technical details, [take a look at the documentation](http://www.evennode.com/docs/node?utm_source=dailyjs&utm_medium=cpc&utm_campaign=promo).  Sign up only requires an email address and password, so you don't even have to hand over credit card details to try it out!

###Mozaik

![Mozaik](/images/posts/mozaik.png)

Mozaik (GitHub: [plouc/mozaik](https://github.com/plouc/mozaik), License: _MIT_, [Demo](http://mozaik.herokuapp.com/)) by Raphaël Benitte is a Node-based web-app for showing dashboards.  It includes some [widgets](https://github.com/plouc/mozaik/wiki/widgets) for CI and monitoring, but you can add more.  It also comes with five themes.  Of course, you can create your own [widgets](https://github.com/plouc/mozaik/wiki/Extend) and [themes](https://github.com/plouc/mozaik/wiki/theming).

Other than the very clear and attractive design, one feature that I liked was rotating dashboard layouts.  This would be cool if you've got multiple teams in the same office that perform different roles.  You could rotate between support information, developer tickets/CI, and server monitoring.

Mozaik is built with React and Express.

###Marko

Marko (GitHub: [raptorjs/marko](https://github.com/raptorjs/marko), License: _Apache 2.0_, npm: [marko](https://www.npmjs.com/package/marko)) by Patrick Steele-Idem is a templating language for Node and browsers that uses HTML with custom tags.  It's being used at eBay as part of their Node stack, and it has been covered by some cool blogs like [the StrongLoop blog](http://strongloop.com/strongblog/bypassing-express-view-rendering-for-speed-and-modularity/).

[There's a live demo](http://raptorjs.org/marko/try-online/) where you can try out the syntax.  The markup uses attributes for data binding and iteration, so you can say `if="notEmpty(data.colors)"` and repeat elements with `for="color in data.colors"`.  I haven't seen this syntax before, but I think it would be easy to learn if you're used to declarative template systems.

One thing about Marko that makes a huge amount of sense to me is the fact it's asynchronous.  You can stream output with Node's HTTP response objects, which will fit in extremely well with frameworks like Express.  The design philosophy statement for Marko says "it should be possible to render HTML out-of-order, but the output HTML should be streamed out in the correct order", and I think this is extremely useful.

The documentation is great and you can extend it with custom [tag libraries](https://github.com/raptorjs/marko#custom-taglibs) -- why not [try it out now](http://raptorjs.org/marko/try-online/)?
