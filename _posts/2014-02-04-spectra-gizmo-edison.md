---
layout: post
title: "Spectra, GizmoJS, EdisonJS"
author: Alex Young
categories:
- jquery
- design
---

###Spectra

[Spectra](http://aakpat6.github.io/spectra/) (GitHub: [aakpat6 / spectra](https://github.com/aakpat6/spectra), License: _MIT_, npm: [spectra](https://npmjs.org/package/spectra)) by Aakash Patel is a library for working with colours.  It's a function that accepts various colour formats: RGB, HSL, hex, and CSS colour names.

It can also convert formats, so calling `colour.hex()` will return a hex value.  Colours can even be compared with the `.equals` method.  There are additional methods for processing colours, including `harmony`, which can generate harmonies for analogous, triad, complementary, square, and rectangle colours.

The [Spectra API documentation](http://aakpat6.github.io/spectra/) has examples for each method, and the author has included unit tests.

###EdisonJS

EdisonJS (GitHub: [tkambler / edison.js](https://github.com/tkambler/edison.js), License: _MIT_) by Tim Ambler is a router for single page applications based on hierarchical relationships.  The idea is to define sections and routes.  Sections contain routes, and routes map to URLs.  That means visiting a URL will cause a section's callback to fire.

The API is based around instances of sections that you define with `edison.createSection`.  There's also a `edison.extendCleanup` method that fires when people navigate away from routes.

###GizmoJS

Tim Ambler also sent in GizmoJS (GitHub: [tkambler / gizmo](https://github.com/tkambler/gizmo), License: _MIT_, Bower: _gizmo_).  GizmoJS is a component library, similar to jQuery UI's widget factory.  It doesn't depend on jQuery, but does need RequireJS, because the components are based on AMD.  It has an event API and inheritance helper.
