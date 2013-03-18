---
layout: post
title: "OrganicJS, HALbert, BromBone"
author: Alex Young
categories: 
- node
- libraries
- graphics
- frameworks
- api
---

###OrganicJS

[OrganicJS](http://idibidiart.github.com/organicjs/) (GitHub: [idibidiart / organicjs](https://github.com/idibidiart/organicjs)) by Marc Fawzi is a reusable component framework, which combines ideas from the author's previous work with D3.js.  It supports chainable properties, dynamic getters and setters, reusable and nestable markup, in-place fragment cloning and rendering, and decoupled data/behaviour sharing across components.

The project is currently in an early state, without much documentation or tests, but Marc is looking for feedback on the project.  If you want to try it out, the best way to get started is by looking at the [OrganicJS demo site](http://idibidiart.github.com/organicjs/).

###HALbert

HALbert (GitHub: [xcambar / halbert](https://github.com/xcambar/halbert), License: _MIT_, npm: [halbert](https://npmjs.org/package/halbert)) by Xavier Cambar is a [HAL-JSON](http://tools.ietf.org/html/draft-kelly-json-hal-05) parser:

> There is an emergence of non-HTML HTTP applications ("Web APIs") which use hyperlinks to direct clients around their resources.

> The JSON Hypertext Application Language (HAL) is a standard which establishes conventions for expressing hypermedia controls, such as links, with JSON [RFC4627].

> HAL is a generic media type with which Web APIs can be developed and exposed as series of links.  Clients of these APIs can select links

It can be used as a Node module or in browsers, through [Browserify](https://github.com/substack/node-browserify).  The author has designed it to work pretty much anywhere in your application's stack: Express middleware, or in client-side frameworks like Backbone or AngularJS.

###BromBone

Although PhantomJS is extremely useful, there are times when you don't want to include the dependency in a server-side project.  I've considered making my own mini REST services for such cases, so the "heavier" dependencies like PDF generation or PhantomJS are split off into their own self-contained projects.  But why bother building such services at all?  Surely there are suitable APIs that can be used from services like Heroku and Nodejitsu?

Enter [BromBone](http://www.brombone.com/), by Chad DeShon.  BromBone is a web service for PhantomJS, with a [simple API](http://www.brombone.com/#try) and [reasonable pricing](http://www.brombone.com/#pricing).  It currently allows a page to be rendered as a PNG with an optional delay, and can also run JavaScript on a page.  Chad only released the project recently so he's looking for new users to try it out.
