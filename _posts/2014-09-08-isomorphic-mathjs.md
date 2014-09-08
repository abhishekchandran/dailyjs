---
layout: post
title: "From AngularJS to React, Math.js 1.0"
author: "Alex Young"
categories:
- angularjs
- maths
- react
---

###From AngularJS to React: The Isomorphic Way

Gergely Nemeth sent in [From AngularJS to React: the isomorphic way](http://blog.risingstack.com/from-angularjs-to-react-the-isomorphic-way/), which outlines how his company used React, Flux, and Koa to reuse code in the browser and on the server.  The server-side code is capable of generating a Flux-React application instance and then rendering views.

> The browser loads the same code (built with Browserify/Webpack) and bootstraps the application from the shared state. (shared by the server and injected into the global/window scope). This means that our application can continue from the point where the server has finished.

It seems like a lot of people struggle to share code this way, so it's interesting to see how the author's Angular experiences compared with React.

###Math.js 1.0

Jos de Jong sent us an email to say [Math.js](http://mathjs.org/docs/getting_started.html) has been updated to version 1.0.  The project now has more tests and BigNumber support.

[There are more examples](http://mathjs.org/examples/index.html) so you can see cool features like [chained operators](http://mathjs.org/examples/chained_operations.js.html) and [function transforms](http://mathjs.org/examples/function_transform.js.html).

You can create BigNumbers with strings, like this:

{% highlight javascript %}
math.config({
  number: 'bignumber',
  precision: 20 // Number of significant digits for BigNumbers
});

math.bignumber('1.2e+500');  // BigNumber, 1.2e+500
{% endhighlight %}

Jos is working on some new features, including derived units (like `km/h`, `kg*m/s^2`), and performance improvements.  He also wanted to thank the JavaScript community for helping with the project:

> I want to thank the community for all valuable and constructive feedback and discussions. Without them, I don't think we would have had an API so elegant and consistent as it is now. I'm looking forward to the coming period, implementing more great features, making math.js better and better.

