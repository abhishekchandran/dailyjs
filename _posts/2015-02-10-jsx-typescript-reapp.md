---
layout: post
title: "JSX-TypeScript, Reapp"
author: Alex Young
image: "/images/posts/reapp.png"
categories:
- node
- modules
- libraries
- react
- typescript
---

###JSX-TypeScript

JSX-TypeScript (GitHub: [fdecampredon/jsx-typescript](https://github.com/fdecampredon/jsx-typescript), License: _Apache 2.0_, npm: [jsx-typescript](https://www.npmjs.com/package/jsx-typescript)) by François de Campredon is a fork of TypeScript that allows you to use React's JSX syntax.  There's a port of the [TodoMVC that uses JSX-TypeScript](https://github.com/fdecampredon/react-typescript-todomvc) that shows how it works.  The [app.ts](https://github.com/fdecampredon/react-typescript-todomvc/blob/master/src/main/app.ts) file, for example, has fragments of JSX in a `render` method, just like a typical React application.

Because React seems influenced by some of the trends in the modern .NET world, the marriage of TypeScript and React seems like an obvious move, and it may appeal to people who like React but would like to try TypeScript.

###Reapp

![Reapp](/images/posts/reapp.png)

[Reapp](http://reapp.io/) (GitHub: [reapp/reapp](https://github.com/reapp/reapp), License: _MIT_, npm: [reapp](https://www.npmjs.com/package/reapp)) is a new React-based UI toolkit for making mobile applications that feel more like native apps. It uses ES6 modules, and comes with a command-line tool for managing projects, so you can create a quick test app without too much trouble.

The authors say it isn't a framework, but it does come with a set of modules that makes React and ES6 more accessible:

> What we found was this: if you can subscribe so a certain file structure, you can avoid the framework. With that file structure, we can provide helpers via a CLI. Bootstrap your app in one command and you have a mature build system built in, without having to do anything.

The project's features and future goals are a good mix of web and mobile technologies: it has a fast animation API, with support for themes, and React modules for things like routing. The mobile-style views and widgets remind me of `UIView` in iOS, in terms of API and look and feel. The [UI documentation](http://reapp.io/ui.html) has an overview of the various widgets, including popovers, menus, and titlebars.

It's still billed as an alpha release, but I think Reapp seems like a very useful blend of UI components and React utilities that could be used for rapid mobile development.

