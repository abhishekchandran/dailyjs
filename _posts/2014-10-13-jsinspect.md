---
layout: post
title: "Compare Code Similarity with jsinspect"
author: "Alex Young"
image: "/images/posts/jsinspect.png"
categories:
- node
- modules
- libraries
- code-quality
---

![jsinspect](/images/posts/jsinspect.png)

jsinspect (GitHub: [danielstjules / jsinspect](https://github.com/danielstjules/jsinspect), License: _MIT_, npm: [jsinspect](https://www.npmjs.org/package/jsinspect)) by Daniel St. Jules is a tool for detecting copy-pasted and structurally similar JavaScript.  It also detects boilerplate and repeated logic, so you could use it to extract code into methods or help find dead code.

Installing it with npm gets you a command-line tool that can be used to analsyse multiple paths.  You could also use it as part of a project's build process, perhaps during a linting phase.  I ran it on the source to [Ghost](https://github.com/TryGhost/Ghost), and it found matches in the server code between password reset and invitations, which makes sense.  The command I used was `jsinspect -t 30 -i core/server`.

This project is based on the [Acorn](https://www.npmjs.org/package/acorn) ECMAScript parser.  Acorn is used to generate lists of nodes that are compared based on a similarity threshold (set by `-t`).

> You have the freedom to specify a threshold determining the smallest subset of nodes to analyze. This will identify code with a similar structure, based on the AST node types, e.g. BlockStatement, VariableDeclaration, ObjectExpression, etc. For copy-paste oriented detection, you can even limit the search to nodes with matching identifiers.

For bonus points, you can try combining jsinspect with a script that searches for the copied code on Stack Overflow!
