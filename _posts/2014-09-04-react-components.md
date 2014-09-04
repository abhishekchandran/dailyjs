---
layout: post
title: "React Components"
author: "Alex Young"
categories:
- modules
- node
- libraries
---

![React Components](/images/posts/reactcomponents.png)

In the Node community, frontend package managers are regarded with suspicion.  I've worked on projects that manage client-side dependencies with both Bower and npm, and although Bower does an admirable job I often feel like I should be using npm instead.  That's mainly because I always have to add a step where client-side files are preprocessed and moved from where Bower downloads them, so it's not really much different to accessing the same files in `node_modules`.

[React Components](http://react-components.com/) (GitHub: [vaffel / react-components](https://github.com/vaffel/react-components), License: _MIT_) from VaffelNinja is a database of React components based on data on npm.  It works by assuming React modules are tagged with `react-component`.

It has a few UI touches that makes it friendly and useful:

* Searching is real time
* The URL is dynamically updated with the search term
* You can copy and paste the URL with the search term
* Modules render the readme and the most useful links (GitHub, homepage)

This project is a great example of how npm can be completely appropriate for client-side modules, and also highlights how many interesting React components are being created right now.
