---
layout: post
title: "jsEq, Angular-breadcrumb"
author: "Alex Young"
categories:
- angularjs
- equality
---

###jsEq

jsEq (GitHub: [loveencounterflow / jseq](https://github.com/loveencounterflow/jseq), License: _ISC_) is a deep equality test suite:

> There are a couple of related, recurrent and, well, relatively 'deep' problems that vex many people who program in JavaScript on a daily base, and those are sane (deep) equality testing, sane deep copying, and sane type checking.

It highlights how much variance there is between different equality implementations, including lodash, Underscore, Node's `assert.deepEqual`, and more.

The project uses dependencies from npm, so even though it uses lots of dependencies it's easy to install and run the tests.

The readme has a list of axioms that are used to design the tests.  So far, Underscore and lodash seem to be winning:

> I sorted the results, and seeing that underscore got the highscore (pun intended), it surprised me to see that it insisted on treating +0 and -0 as not equal. Ultimately, this led to the discovery of the second Axiom, and with that in my hands, it became clear that underscore got this one right and my test case got it wrong: Since there are known programs that behave differently with positive and negative zero, these two values must not be considered equal.

The output of the test suite looks incredibly cool -- you can easily see the output of a huge amount of tests.  There's a glorious console screenshot in the readme.

###Angular-breadcrumb

Angular-breadcrumb (GitHub: [ncuillery / angular-breadcrumb](https://github.com/ncuillery/angular-breadcrumb), License: _MIT_) by Nicolas Cuillery is a module for generating breadcrumb navigation.  You can use the `ncy-breadcrumb` directive to apply it.

It's based on the [AngularUI Router](https://github.com/angular-ui/ui-router), and Nicolas has been writing pretty solid documentation in the [Angular-breadcrumb wiki](https://github.com/ncuillery/angular-breadcrumb/wiki).
