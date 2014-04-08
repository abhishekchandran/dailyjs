---
layout: post
title: "AngularJS Localization"
author: "Alex Young"
categories:
- ui
- libraries
- AngularJS
---

Sebastian Tschan, also known as blueimp, is the author of the hugely popular [jQuery-File-Upload](http://blueimp.github.io/jQuery-File-Upload/) project.  It turns out he also writes AngularJS modules.  His recent AngularJS project is dedicated to localization, and works well with a Grunt task that builds locales:

* [angular-localize](https://github.com/blueimp/angular-localize) (License: _MIT_, npm: [angular-localize](https://www.npmjs.org/package/angular-localize)) provides a localization directive
* [grunt locales](https://github.com/blueimp/grunt-locales) (License: _MIT_, npm: [grunt-locales](https://www.npmjs.org/package/grunt-locales)) parses `localize` attributes in HTML files

By running `grunt locales:build` you can get a set of JavaScript locale files that can be used to help translate content.

The basic angular-localize directive is used by adding the `localize` attribute to a tag.  The text in the element will be used as the translation key, but you can use `localize="key"` to specify the key instead, which is useful if the final content hasn't yet been copy edited.

The `localize` directive also observes `data-*` attributes and passes them as objects to translation functions, so data can be inserted into text dynamically.

There's also a `localize` service for translating text in your JavaScript code, and there's even a `localizeFactory` for creating your own attribute-based `localize` directives.
