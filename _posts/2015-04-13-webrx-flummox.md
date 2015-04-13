---
layout: post
title: "WebRx, Flummox"
author: Alex Young
categories:
- react
- reactive
- libraries
- frameworks
---

### WebRx

Oliver Weichhold sent in [WebRx](http://webrxjs.org) (GitHub: [oliverw/WebRx](https://github.com/oliverw/WebRx), License: _MIT_), a new MVVM framework built on [ReactiveX for JavaScript](http://reactivex.io).  It combines ideas from several libraries, including a router inspired by Angular's UI-Router, and bindings inspired by Knockout.  It also supports [dependency injection](http://webrxjs.org/docs/dependency-injection-overview.html#start), [components](http://webrxjs.org/docs/component-overview.html#start), modules, and routing.

The choice of patterns and JavaScript idioms means you get an interesting blend of Angular, Knockout, and Rx.  If you're an Rx or TypeScript developer then it may appeal to you.  It might even work if you're using Knockout with plain old JavaScript but want to move to a framework to aid with your application's architecture.

###Flummox

Asaf Katz sent in [Flummox](http://acdlite.github.io/flummox) (GitHub: [acdlite/flummox](https://github.com/acdlite/flummox), License: _MIT_, npm: [flummox](https://www.npmjs.com/package/flummox)) by Andrew Clark.  Flummox is a Flux library that provides higher-level encapsulation: you can combine all of your stores, actions, constants, and the dispatcher into a single class.  The class has no global references or singletons, which seems ideal for testing.  The author argues that this makes isomorphism more straightforward -- imagine being able to load the same module on the client and server without any messy internal dependencies and state.

> The primary goal of Flummox is reduce the boilerplate involved in setting up Flux for your application, so the API has been kept as minimal and predictable as possible. It uses Facebook's dispatcher under the hood. It encourages (but does not require) the use of ES6 classes. The state API for stores mirrors the state API for React components. Everything works as you'd probably expect.

Using Flummox with React requires adding event listeners, but Andrew recommends doing this with FluxComponent or fluxMixin.

