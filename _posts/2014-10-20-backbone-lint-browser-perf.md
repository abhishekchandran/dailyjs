---
layout: post
title: "Linting Backbone Apps, Hybrid Mobile Performance"
author: "Alex Young"
image: "/images/posts/hybrid-perf.png"
categories:
- backbone
- performance
- mobile
---

###eslint-plugin-backbone

eslint-plugin-backbone (GitHub: [ilyavolodin / eslint-plugin-backbone](https://github.com/ilyavolodin/eslint-plugin-backbone), License: _MIT_, npm: [eslint-plugin-backbone](https://www.npmjs.org/package/eslint-plugin-backbone)) by Ilya Volodin is a Backbone-specific ESLint plugin.  It can verify collections and views, which will help you find common mistakes like direct jQuery usage inside views.

Each of the rules is documented, and the documentation describes when _not_ to use the rule as well.  This is good if you're hitting a lot of linter errors for specialised behaviour that should be ignored.

Because the rules are so well documented you might like to use it to brush up on your Backbone best practices as well.

###Hybrid Mobile Performance with browser-perf

If you're developing cross-platform apps powered by technologies like Cordova, how do you benchmark them? [browser-perf](https://www.npmjs.org/package/browser-perf) by Parashuram is a Node module for gathering rendering performance metrics.  The author has recently published a blog post called [Cordova Apps - Rendering Performance](http://blog.nparashuram.com/2014/10/measuring-rendering-performance-metrics.html) that describes how to use browser-perf with hybrid mobile apps.

> When developing a mobile app, one of the concerns of using the Hybrid approach is performance. Achieving smooth experience like a native app is important for Hybrid apps and developer tools for Android and iOS have been helping to a great deal.

For Android, Chromedriver is used with the Selenium JSON wire protocol.  iOS uses Appium, but Parashuram had to [enable performance logs](https://github.com/appium/appium/pull/3530) before this worked.

