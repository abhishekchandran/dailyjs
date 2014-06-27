---
layout: post
title: "Node Roundup: husky, grunt-npmcopy"
author: "Alex Young"
categories:
- node
- modules
- npm
- grunt
- git
---

###husky

husky (GitHub: [typicode / husky](https://github.com/typicode/husky), License: _MIT_, npm: [husky](https://www.npmjs.org/package/husky)) by typicode is a module for helping to avoid bad commits being pushed using Git hooks.

It basically sets up Git hooks for your Node projects:

> So what makes husky different?
> 
> First, other modules often replace or delete existing hooks.
> husky won't ever replace or modify an existing hook, so it's a safer choice for a team or an open source project. In other terms, people who have set up their own hooks won't be impacted by husky.
> 
> I think also that husky is more easier and straightforward to use compared to others. husky's README is just a few lines and setting up hooks should be simple.
> 
> And last, usually other modules introduces unconventional package.json fields, husky uses only valid package.json fields.

###grunt-npmcopy

grunt-npmcopy (GitHub: [timmywil / grunt-npmcopy](https://github.com/timmywil/grunt-npmcopy), License: _MIT_, npm: [grunt-npmcopy](https://www.npmjs.org/package/grunt-npmcopy)) by Timmy Willison allows you to use the same package manager for Node and client-side projects.  It helps place client-side dependencies in the right directory by using a Grunt task called `npmcopy`.

The `npmcopy` task takes source and destination options so you can avoid copying lots of extra files into your publicly accessible asset directories.

> Have you ever wondered why we have so many package managers? NPM, Bower, Component. Why don’t we just pick one? Well, after much deliberation with developers like you, I’ve decided to support the idea that NPM might just be able to handle it all.

