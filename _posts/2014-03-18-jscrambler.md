---
layout: post
title: "JScrambler"
author: Ricardo Martins
categories:
- sponsored-content
- obfuscation
- services
---

<div class="sponsored-content">
  <p><a class="label" href="/sponsored-content.html">Sponsored Content</a> This post is about a commercial product that we think will appeal to DailyJS readers.</p>
</div>

<div class="image">
  <img src="/images/posts/jscrambler.png" />
  <small>JScrambler.</small>
</div>

Well-known libraries such as Google Closure, YUI compressor or UglifyJS minify, compress and optimize JavaScript. The techniques they use can be collectively referred to as _JavaScript optimization_. They are great at improving overall page load speed, but fall short if you are interested in protecting your source code from code theft and reuse, tampering, or reverse engineering.

Despite that, optimized code is often confused with obfuscated code. For example, compressed code is completely encoded, which at first glance may seem to be highly obfuscated, but a simple run is often enough to retrieve something very similar to the original code. In short, these tools do a good job optimizing your code, but they don't protect it. (fiddle: [demo](http://jsfiddle.net/JScrambler/GaeLD/), [Google Compiler optimized demo](http://jsfiddle.net/JScrambler/Dtna2/) and [beautified optimized demo](http://jsfiddle.net/JScrambler/k5vLc/)).

[JScrambler](https://jscrambler.com/) goes beyond these libraries by offering advanced obfuscation ([JScrambler obfuscated version](http://jsfiddle.net/JScrambler/Q6QMg/)) that can protect your code. It leverages obfuscation by inserting a number of different code traps to control execution and to enforce licensing. For example, you can lock the code to a list of predefined domains. If someone tries to execute the code elsewhere, the code breaks.

JScrambler just released a new version (3.5) that takes protection even more seriously. It introduces a completely new technique that provides JavaScript files with _self-defending_ capabilities by installing a combination of anti-tampering and anti-debugging. If you try to change a single character, the code will react by breaking down intentionally (try it on [JScrambler self-defending demo](http://jsfiddle.net/JScrambler/5ujp3/)). It also adds new code traps to restrict execution to a certain Browser or OS, _code blocks_ to give the developer the ability to enable/disable individual source code transformations in certain parts of the code.

There are lots of reasons why you may want to protect your code. People might try to steal your code to reuse it, perhaps to build a similar product, or to replicate a similar user experience. You may have secret algorithms or keys hidden in the code that may be easily recovered by inspecting your code. If you are selling your app, you may be worried about piracy. JavaScript can be easily copied and executed, without your authorization. And last but not least, there are all sorts of security risks, like people figuring out ways to interfere with your code, to commit fraud, or to steal data -- from you, or from your users. JScrambler goes along way to combating these problems, despite the fact that there are no bulletproof solutions.

As expected, these techniques have a cost in file size and execution, but because JScrambler also has optimization features, this extra cost can be controlled -- as proven by running the two protected demos. You don't have to give up performance to get protection.

JScrambler's web interface is simple and easy to use. In five minutes you can get your application protected.  You upload the source, click a button, then wait a few seconds and download the results. JScrambler provides templates that were designed to work out of the box in most cases. It includes all sorts of JavaScript-based applications, including HTML5 Canvas, Node.js, Windows 8 WinJS Apps, etc. If you want to automate your builds, an API is also provided, and few ready to use clients, including a [Node grunt task](https://github.com/auditmark/grunt-jscrambler).

For more examples, see the [full set on jscrambler.com](https://jscrambler.com/en/examples).
