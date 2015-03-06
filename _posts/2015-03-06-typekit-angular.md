---
layout: post
title: "Angular 2 and TypeScript, Comparing Angular 1.x and 2.0"
author: Alex Young
categories:
- angular
- typescript
---

###Angular 2 is Built on TypeScript

There's a post on the msdn blog that says [Angular 2.0 is built with TypeScript](http://blogs.msdn.com/b/typescript/archive/2015/03/05/angular-2-0-built-on-typescript.aspx).  This is a big step, but there is a precedent for it -- [an earlier Angular blog post mentioned the AtScript project](http://angularjs.blogspot.co.uk/2014/10/ng-europe-angular-13-and-beyond.html) that resulted in a collaboration between [Microsoft and the Angular team](http://blogs.msdn.com/b/typescript/archive/2014/10/22/typescript-and-the-road-to-2-0.aspx).

> This partnership has been very productive and rewarding experience for us, and as part of this collaboration, we're happy to announce that Angular 2 will now be built with TypeScript.  We're looking forward to seeing what people will be able to do with these new tools and continuing to work with the Angular team to improve the experience for Angular developers.

Now AtScript development has been abandoned in favour of TypeScript, what does this mean for Angular developers?  There's a [TodoMVC TypeScript Angular 2.0 example project on GitHub](https://github.com/davideast/ng2do/blob/master/todo.js), which uses JavaScript for the main code.  To use it, you'll need to download the new Angular 2.0 code separately.

Hopefully this shift will result in a more future-proof Angular, but it's hard to tell if switching to TypeScript now is a good idea, given the interest in ES6 and ES7.

###Comparing Angular 1.x and 2.0

In case you're excited/worried/apathetic about the previous news, Shawn McKay sent in a post that compares [angular 2.0 with 1.x](http://shmck.com/comparing-angular-1-x-2-0/):

> Angular 2.0 looks fantastic. It's not ready yet, but you can play around with it today. Checkout the [GitHub](https://github.com/angular/angular) for more. There are also some examples available, such as [ng2do](https://github.com/davideast/ng2do).

The post explains how to set up Angular 2.0 and outlines the major new features.  If you're also working with React, then you might want to read more about the new DOM handling:

> "2.0: In many ways, Angular 2.0 seems to handle DOM style manipulation with something similar to React.js's virtual DOM, which they referred to in a recent presentation as the "view". In response to a recent question about 'Angular Native?', Misko mentioned that this View could be run on a web worker or even potentially on native."

