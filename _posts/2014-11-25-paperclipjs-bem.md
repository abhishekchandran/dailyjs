---
layout: post
title: "Paperclip.js, bem-react"
author: "Alex Young"
image: "/images/posts/definejs.png"
categories:
- templates
- reactive
- react
---

###Paperclip.js

[Paperclip](http://paperclipjs.com/) (GitHub: [mojo-js/paperclip.js](https://github.com/mojo-js/paperclip.js), License: _MIT_, npm: [paperclip](https://www.npmjs.org/package/paperclip)) by Craig Condon is a template engine that's a bit like React, except it translates HTML templates into JavaScript document fragments rather than using a virtual DOM.  The template is then cloned when it's used, and `requestAnimationFrame` is used to prevent unnecessary DOM operations.

Craig provided some examples so you can see how it compares to other projects:

* Partial todomvc: <http://paperclip-todomvc-example.herokuapp.com/>
* Angular fast-repeat directive: <http://plnkr.co/edit/dgalyKuVqJdfKLGJNdnm?p=preview>
* Updating 1000 items: <http://requirebin.com/?gist=425cdb646205bb819477>

Paperclip has been used for two years in production at [ClassDojo](https://www.classdojo.com/), so it sounds battle tested.  It has unit tests that run in browsers and Node, and you can also use the module itself in Node.

###bem-react

bem-react (GitHub: [dfilatov/bem-react](https://github.com/dfilatov/bem-react), License: _MIT_, Bower: _bem-react_, npm: [bem-react](https://www.npmjs.org/package/bem-react)) is a module for React that provides features to support the [BEM methodology](http://bem.info/method/) which was developed by Yandex.

> BEM is a methodology of web projects development, that allows you to divide an interface into logically independent blocks. At the same time BEM contains specific tools for the typical web developers' tasks automatization. And finally BEM gives us opportunity to create libraries of web-components for fast and efficient web-development.


With this module, you can use "bemjson" in templates instead of jsx or JavaScript, and manipulate CSS classes based on BEM.

I noticed there's a demo app in [bem-react/example](https://github.com/dfilatov/bem-react/tree/master/example) that highlights the bemjson special fields, component use, and component composition.
