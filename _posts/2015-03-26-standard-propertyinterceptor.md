---
layout: post
title: "Standard, propertyinterceptor"
author: Alex Young
categories:
- node
- libraries
- modules
- style
- es6
---

###Standard

Feross Aboukhadijeh's Standard (GitHub: [feross/standard](https://github.com/feross/standard), License: _MIT_, npm: [standard](https://www.npmjs.com/package/standard)) is a zero config linter that checks your code against community conventions:

> Adopting standard style means ranking the importance of community conventions higher than personal style, which does not make sense for 100% of projects and development cultures. At the same time, open source can be a hostile place for newbies. Setting up clear, automated contributor expectations makes a project healthier.

Be aware that one of the choices is no semicolons, which I don't believe is popular enough to be considered a "community convention".  However, key contributors in the Node community do advocate dropping semicolons, so things seem to be moving that way.

This project uses eslint and contains the `.eslintrc` file so you don't have to worry about it.  In fact, the idea of settling on a standard style guide for a project is sensible and something that can be automated rather than left to the PR/code review stage.

###propertyinterceptor

If you use [Object.getOwnPropertyDescriptor](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/getOwnPropertyDescriptor) and [Object.defineProperty](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty) then you might like Simon Blackwell's propertyinterceptor (GitHub: [anywhichway/propertyinterceptor](https://github.com/anywhichway/propertyinterceptor), License: _MIT_, npm: [propertyinterceptor](http://npmjs.com/package/propertyinterceptor)):

> A simple, standardized means of creating reliable chained before and after methods on Javascript object properties for validation, security, functional reactive programming, and more.

It adds the following methods:

* `Object.intercept.afterGet(someObject,someProperty,interceptor)`
* `Object.intercept.beforeSet(someObject,someProperty,interceptor)`
* `Object.intercept.afterSet(someObject,someProperty,interceptor)`

You can also short circuit the interceptor chain by throwing an `Error` object.  If you like `getOwnPropertyDescriptor` or `defineProperty` but dislike the boilerplate, then you might prefer Simon's API.

