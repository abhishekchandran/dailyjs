---
layout: post
title: "Node Roundup: npm's New Web Framework, Notes from the Road, TJ Fontaine Interview"
author: "Alex Young"
categories:
- node
- modules
- npm
- interviews
---

###npm's New Web Framework

In [Nearing Practical Maintainability](http://blog.npmjs.org/post/88024339405/nearing-practical-maintainability) on the official npm blog, there's a discussion about the decision to use [hapi.js](http://hapijs.com/) for npm's new site:

> Both Hapi and Express rate extremely well against our juding criteria. To choose between the two, it pretty much came down to the framework architecture: Hapi's plugin system means that we can isolate different facets and services of the application in ways that would allow for microservices in the future. Express, on the other hand, requires a bit more configuration to get the same functionality (it's certainly capable!).

The current [npm-www](https://github.com/npm/npm-www) has a lot of dependencies that you might have seen before: browserify, uglifyjs, moment, ejs, and nodemailer are all popular modules.  I think using something like hapi.js or Express makes sense, even if it just gives the project some architectural hints.

> While, yes, we could use barebones Node.js and roll our own framework, we want to avoid the same "special snowflake" situation that we're currently in. Plus, by using a framework, we can focus more on pushing out the features our community wants and needs, instead of debugging some weird nook and/or cranny that someone forgot about.

###Notes from the Road

[Notes from the Road](http://blog.nodejs.org/2014/06/11/notes-from-the-road/) is a post on Node's official blog by TJ Fontaine about the _Node on the Road_ events:

> These Node on the Road events are successful because of the incredible support from the community and the existing meetup organizations in their respective cities. But the biggest advantage is that the project gets to solicit feedback directly from our users about what is and isn't working for them in Node.js, what modules they're using, and where they need Node to do better.

From these experiences TJ has written up some notes about Node's release schedule, future documentation improvements, and the path to becoming a Node contributor:

> In an effort to make it easier for users to contribute to Node.js the project has decided to lift the requirement of signing the CLA before contributions are eligible for integration. Having to sign the CLA could at times be a stumbling block for a contribution. It could involve a long conversation with your legal department to ultimately contribute typo corrections.

###TJ Fontaine Interview

Meanwhile, the Node hosting company Modulus has [interviewed TJ Fontaine](http://blog.modulus.io/tj-fontaine-interview), where some of these points are reiterated:

> If you're looking for ways to contribute to Node itself, the website will be soon be going through an overhaul to improve our documentation. We're going to be adding a lot more documentation, cleaning up what we already have, as well as designing the pieces to help internationalize the site. Node's community is globally diverse, we should be working to enable Node users everywhere they are.

