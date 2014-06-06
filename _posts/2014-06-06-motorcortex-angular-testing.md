---
layout: post
title: "MotorCortex.js, Testing AngularJS with Jasmine"
author: "Alex Young"
categories:
- animation
- jasmine
- testing
- angularjs
---

###MotorCortex.js

> Think of dancer dancing or a human just walking the street. It is extremely unnatural to think that each part of the body acts independently. A centralized mechanism controls all parts in order to produce a smooth, elastic and natural movement. The "motor cortex", is the specific part of the brain that does exactly this job.

The idea of declarative templates seems to be spilling into the world of client-side animation.  [MotorCortex.js](http://motorcortexjs.com/) (GitHub: [andreas-trad / motorcortexjs](https://github.com/andreas-trad/motorcortexjs), License: _WTFPL_) by Andreas Trantidi is a new library that builds on Velocity.js to provide an animation API that's based on CSS syntax.

With MotorCortex.js, external `*.mss` files determine animation parameters.  These are based on the CSS parameters that are supported by Velocity.js:

{% highlight css %}
.section:myEvent{
  duration: 400;
  top: 300px;
}
{% endhighlight %}

For more examples with the associated CSS and JavaScript, see <http://motorcortexjs.com/#examples>.

###Testing AngularJS with Jasmine

David Posin sent in [Angular and Jasmine: Injecting into the test environment](http://randomjavascript.blogspot.co.uk/2014/06/angular-and-jasmine-injecting-into-test.html).  He's been using Jasmine for tests in both Node and client-side JavaScript, so he wanted to use it with Angular as well:

> Angular requires a very specific environment in which to function. The result of that can be a significant amount of boilerplate when creating tests for Angular applications in Jasmine. The good news is that the amount of redundancy can be minimized with careful test organization.

The way he does this is by creating embedded suites:

> The spec file will have one `describe` that contains that spec's entire content. Inner `describe` clauses will be used to manage and break up the tests. Inside of the main over-arching `describe` we will add variables to contain the services that all the clauses will need.

I too find it frustrating to have to switch my preferred test library because of a framework's design, so it's interesting that he managed to get Jasmine working in the end.  It can be quite hard to think the Angular way for relative newcomers.
