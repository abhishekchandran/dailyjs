---
layout: post
title: "Node Roundup: 0.10.8, msfnode, vnc-over-gif"
author: "Alex Young"
categories: 
- node
- modules
- security
- gif
- vnc
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a>.
</div>

###Node 0.10.8

[Node 0.10.8](http://blog.nodejs.org/2013/05/24/node-v0-10-8-stable/) was released last week.  v8, uv, and npm were all upgraded, and there are fixes and improvements to be found in the http, buffer, and crypto modules.  This is the third stable release so far in May.

###msfnode

![Metasploit](/images/posts/metasploit.png)

msfnode (GitHub: [eviltik / msfnode](https://github.com/eviltik/msfnode), License: _GPL 3_, npm: [msfnode](https://npmjs.org/package/msfnode)) by Michel Soisson is a [Metasploit](http://www.metasploit.com/) API client for Node.  Metasploit is a hugely popular penetration testing framework.  This module allows you to use Node to script Metasploit.  The Metasploit API supports things like managing jobs, loading plugins, and interacting with open sessions to compromised systems.

The module provides a `metasploitClient` constructor, which can be passed an object that contains the Metasploit server's details, including `login` and `password`.  The client is event-based, and the project's readme has an example of how to get a login token and make a request against a server.

###vnc-over-gif

Andrey Sidorov sent in vnc-over-gif (GitHub: [sidorares / vnc-over-gif](https://github.com/sidorares/vnc-over-gif), License: _MIT_, npm: [vnc-over-gif](https://npmjs.org/package/vnc-over-gif)), a VNC viewer that uses animated gifs as the data transport.  It currently has no client-side JavaScript, so it acts purely as a means of viewing a VNC session.  The author is interested in expanding it further with an Ajax-based UI.  There's a good background to the project in the [vnc-over-gif FAQ](https://github.com/sidorares/vnc-over-gif/wiki/FAQ).

Although it isn't interactive, it's a great hack -- the code is currently only around 50 lines, which Andrey claims only took 30 minutes to write.
