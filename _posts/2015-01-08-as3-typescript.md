---
layout: post
title: "From AS3 to TypeScript"
author: Alex Young
image: "/images/posts/typescript-logo.png"
categories:
- as3
- typescript
- parsers
---

If you've got existing ActionScript assets but want to migrate them to another language, what do you do?  One possibility is to convert [AS3](http://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/) to [TypeScript](http://www.typescriptlang.org/).  They share similar language features, but are different enough that the process isn't trivial.

There's a project called [AS3toTypeScript](https://github.com/photonstorm/AS3toTypeScript) by Richard Davey that runs through lots of simple replacements, like converting `Boolean` to `bool`.  It's written in PHP and can be used with a web interface.

In [From AS3 to TypeScript](http://jessefreeman.com/articles/from-as3-to-typescript/) by Jesse Freeman, the author converts a game to TypeScript, which seems like a typical task for an ActionScript developer.  He points out that TypeScript works well because of the Visual Studio support, so it makes sense if you're a Microsoft-based developer.

François de Campredon recently sent me [as3-to-typescript](https://github.com/fdecampredon/as3-to-typescript) (License: _Apache_, npm: [as3-to-typescript](https://www.npmjs.com/package/as3-to-typescript)).  This is a Node-based project that includes the [AS3Parser](https://github.com/fdecampredon/as3-to-typescript/blob/master/lib/parser.js) from Adobe.  That means the conversion process actually parses ActionScript and attempts to output syntactically correct TypeScript.

[The tests](https://github.com/fdecampredon/as3-to-typescript/tree/master/test) are fairly minimal given the goals of the project, but they do show what the tool currently supports.  I'm not particularly for or against ActionScript or TypeScript, but as3-to-typescript is a very interesting and useful combination of technologies that might help you find new life for old game code.
