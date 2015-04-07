---
layout: post
title: "React: HotKeys, Google Maps, Dataminr's UI Components"
author: Alex Young
categories:
- react
- libraries
- ui
- keyboard
- maps
---

###HotKeys

Chris Pearce sent in a library for handling hotkeys in React (GitHub: [Chrisui/react-hotkeys](https://github.com/Chrisui/react-hotkeys), License: _MIT_, npm: [react-hotkeys](https://www.npmjs.com/package/react-hotkeys)).  There's a [blog post](http://chrispearce.co/exploring-hotkeys-and-focus-in-react/) with more details on the project:

> With the ability to monitor the 'focus state' of particular elements (where the element may not neccassarily be a direct focus target but simply within the parent tree) it makes it very easy to bind contextual hotkeys.
>
> And using @ccampbell's excelent mousetrap library we are able to declare our hotkeys with very inutitive syntax.
>
> Combining all this you get react-hotkeys which provides a declarative way of binding hotkeys to your React application.

The library itself provides the `HotKeys` element, which has a `keyMap` attribute.  You can bind keys with names like `del` and `backspace` to handlers in your React application.

> The library aims to take the pain out of defining key mappings, knowing when certain components are 'in focus' and which hotkey handlers in the hierarchy should be called while providing a minimal API and getting out the way for the most part.

Correctly handling focus is one of those details that many web applications get wrong, so if you're building anything relatively complex then react-hotkeys should help.

###React Components for Google Maps

Wrapping Google Maps in React seems like a common problem, but is also a good example of a non-trivial case for creating React components.  Zach Pratt sent in the first of a series of articles about React and Google Maps: [React Components for Google Maps – Part 1](http://attackofzach.com/react-components-for-google-maps-part-1/).

> Building React components for use with google maps can present some challenging problems for those who aren’t aware of the basics/quirks of developing with google maps. I aim to shed some light on the fundamentals of how to get the two to play nicely together, and to encourage developing the components in a way that will promote testability.

[Part 2](http://attackofzach.com/react-components-for-google-maps-part-2/) includes code for extending `google.maps.OverlayView` and the React component for managing the map overlay.

###Dataminr's React Components

Armaan Ahluwalia sent in several React components that have been developed at [Dataminr](http://www.dataminr.com).  The react-components repository (GitHub: [dataminr/react-components](https://github.com/dataminr/react-components), License: _MIT_) includes components for a table, search, pie chart, and modal windows.  There's a [demo](http://dataminr.github.io/react-components/src/js/examples/index.html#table) that shows each of the components with some sample data.

The components are all documented and have sample code, so it's pretty easy to get them working in your own projects.  I also noticed that each component has tests as well, which is interesting if you've ever wondered how to write tests for redistributable components.
