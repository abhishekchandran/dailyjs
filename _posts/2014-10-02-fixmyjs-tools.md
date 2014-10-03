---
layout: post
title: "fixmyjs, Front-end Development Tools"
author: "Alex Young"
image: "/images/posts/fixmyjs.png"
categories:
- modules
- libraries
- lint
- design
- chrome
---

###fixmyjs

![fixmyjs](/images/posts/fixmyjs.png)

Sindre Sorhus sent in [fixmyjs](http://goatslacker.github.io/fixmyjs.com/) (GitHub: [jshint / fixmyjs](https://github.com/jshint/fixmyjs), License: _MIT_, npm: [fixmyjs](https://www.npmjs.org/package/fixmyjs)) by Josh Perez.  It automatically rewrites JavaScript based on linting rules.  There's a command-line tool available through npm, and a web version.

It supports things like semi-colon insertion, case correction, missing curly braces, and removes debugger statements.  Sindre said [Addy Osmani wrote an article about it](http://addyosmani.com/blog/fixmyjs/), where he points out some important things that fixmyjs can get wrong:

> As mentioned earlier, the current version of the module uses Escodegen, which rewrites your source and doesn't take into account original styling information (i.e it will strip it). This makes it easier for the author to support complex new rules as they operate with an AST rather than relying on less reliable approaches like string replacement.

You can avoid this by using the `legacy` option.

If you use Atom, then you can install Sindre's [Atom plugin for fixmyjs](https://github.com/sindresorhus/atom-fixmyjs).  It uses `legacy` by default, and can be run on a whole file or a selection.

###56 Expert's Favourite Front-end Tools


Bauke Roesink sent in a [big list of front-end development tools](https://psdtowordpress.com/frontend-development-tools.html), picked by 56 experts.  Coincidentally, I happened to notice Sindre Sorus is on the list.

Several people picked Chrome, probably because the development tools have progressed so much over the last year or so.  It's increasingly common to see people testing design ideas or puzzling over CSS quirks by editing HTML and CSS in the inspector.  I've recently started using the device emulation tab a lot for responsive designs as well.
