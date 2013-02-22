---
layout: post
title: "Discussion: What Do You Want From Components?"
author: Alex Young
categories:
- component
- bower
---

![Yogruntbower... component!](/images/posts/yeoman-etc.png)

Assume for a second that TJ Holowaychuk's [Component](https://github.com/component) project _isn't_ the future.  And then let's say that, due to support from Twitter and Google (through [Yeoman](http://yeoman.io/)), [Bower](http://twitter.github.com/bower/) becomes the de facto tool for managing and installing client-side dependencies.  Whether you're using Yeoman or Bower with another build tool, you're still left with a gap where reusable UI widgets should be.

While Yeoman improves _workflow_, Component also tackles the notion of sharing "widgets" that contain markup, stylesheets, and code.  If you read TJ's tutorials he pushes the idea of _structural markup_ -- stripping away unnecessary markup to leave behind a vanilla slice of templates that can easily be reskinned with CSS.

With more advanced client-side workflows provided by libraries like Backbone.js, RequireJS, and tools like Yeoman and Bower, I feel like moving away from monolithic UI projects is necessary.  While I like to jump start projects with jQuery UI, Bootstrap, Closure Library, or perhaps even Dojo's Dijit and DojoX, these projects are more monolithic than the modular dream promised by the Component project.

I believe there's a missing library to the Bower/Yeoman future: something to support the notion of reusable widgets.  Packaging chunks of markup, styles, and JavaScript is nothing new -- but what is being done to solidify this goal outside of the Component project and older monolithic approaches?

###Standards

The component idea is being formalised in [Introduction to Web Components](https://dvcs.w3.org/hg/webcomponents/raw-file/tip/explainer/index.html), and lists Dominic Cooney and Dimitri Glazkov from Google as the editors.  Therefore, the concept is being standardised, but this particular vision of components seems very different to what TJ and other developers have envisioned.

###Accessibility

Should a widget/component library enforce [ARIA](http://www.w3.org/WAI/intro/aria.php), or provide tools for making accessible components?  jQuery UI went through many iterations to improve its accessibility, and Dojo has documentation on [creating accessible widgets](http://dojotoolkit.org/reference-guide/1.8/quickstart/writingWidgets/a11y.html).

###Data Binding APIs

What about data binding or MVC style development?  How would UI components fit in?  If you're shipping JavaScript inside a component, how would the API provide hooks that can work with Knockout, AngularJS, and other libraries without manually plugging them in?

It feels like we're settling on binding using `data-` attributes, so this might be relatively trivial in practice.  Perhaps the "ultimate" component library would address this, or perhaps it's unnecessary.

###What Do You Want?

Let's say you settle on Yeoman as your workflow tool for client-side development.  What do **you** think reusable client-side widgets should look like?  What would be the perfect fit alongside Yeoman, Bower, Grunt, and a data binding library?

