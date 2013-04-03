---
layout: post
title: "Node Roundup: 0.11.0, Dependo, Mashape OAuth, node-windows"
author: "Alex Young"
categories: 
- node
- modules
- dependencies
- oauth
- authentication
- windows
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a>.
</div>

###0.11.0, 0.10.2

[Node 0.11.0](http://blog.nodejs.org/2013/03/28/node-v0-11-0-stable/) has been released, which is the latest unstable branch of Node.  Node [0.10.12](http://blog.nodejs.org/2013/03/28/node-v0-10-2-stable/) was also released, which includes some fixes for the `stream` module, an update for the internal uv library, and various other fixes for cryptographic modules and `child_process`.

###Dependo

![Dependo](/images/posts/dependo.png)

Dependo (GitHub: [auchenberg / dependo](https://github.com/auchenberg/dependo), License: _MIT_, npm: [dependo](https://npmjs.org/package/dependo)) by Kenneth Auchenberg is a visualisation tool for generating force directed graphs of JavaScript dependencies.  It can interpret CommonJS or AMD dependencies, and uses [MaDGe](https://github.com/pahen/node-madge/) to generate the raw dependency graph.  [D3.js](http://d3js.org/) is used for drawing the results.

###Mashape OAuth

Mashape OAuth (GitHub: [Mashape / mashape-oauth](https://github.com/Mashape/mashape-oauth), License: _MIT_, npm: [mashape-oauth](https://npmjs.org/package/mashape-oauth)) by Nijiko Yonskai is a set of modules for OAuth and OAuth2.  It has been designed to work with lots of variations of OAuth implementations, and includes some lengthy Mocha unit tests.

The authors have also written a document called [The OAuth Bible](https://github.com/Mashape/mashape-oauth/blob/master/FLOWS.md) that explains the main concepts behind each supported OAuth variation, which is useful because the OAuth terminology isn't exactly easy to get to grips with.

###node-windows

node-windows (GitHub: [coreybutler / node-windows](https://github.com/coreybutler/node-windows), License: _MIT/BSD_, npm: [node-windows](https://npmjs.org/package/node-windows)) by Corey Butler is a module designed to help write long-running Windows services with Node.  It supports event logging and process management without requiring Visual Studio or the .NET Framework.

> Using native node modules on Windows can suck. Most native modules are not distributed in a binary format. Instead, these modules rely on npm to build the project, utilizing node-gyp. This means developers need to have Visual Studio (and potentially other software) installed on the system, just to install a native module. This is portable, but painful... mostly because Visual Studio itself is over 2GB.

> node-windows does not use native modules. There are some binary/exe utilities, but everything needed to run more complex tasks is packaged and distributed in a readily usable format. So, no need for Visual Studio... at least not for this module.

