---
layout: post
title: "Worth Starring: Components"
author: "Alex Young"
categories:
- libraries
- client-side
- starred
---

Back in July, [TJ Holowaychuk wrote a post entitled Components](http://tjholowaychuk.com/post/27984551477/components) in which he outlined an approach to JavaScript project distribution.  In the post he discusses CSS and the relationship with modernisation, asset bundling and packaging, require fragmentation and package distribution, and the potential move away from libraries like jQuery in the future.

<div class="image">
  <img src="/images/posts/tjcomponent.png" alt="" />
  <small>An example of a <a href="https://github.com/component/calendar">calendar</a> component.</small>
</div>

Almost four months later I found myself wondering what TJ and his collaborators had done since then.  I was surprised to find 123 public repositories in the [component GitHub account](https://github.com/component).  There are repositories with updates as recent as a day ago.

It's impressive how many of the repositories are truly generic, given the number of them.  For example, [enumerable](https://github.com/component) helps iterate over sets of objects -- a very focused slice of [Underscore's](http://underscorejs.org/) functionality.  Other repositories are reminiscent of popular jQuery plugins, and come bundled with cut-down CSS and structural markup, as promised by TJ's post.  The [menu](https://github.com/component/menu) component is a good example of this.

There's also a [search-api](https://github.com/component/search-api) repository for the component registry.

TJ attempted to formalise the structure of components in the [Component Spec](https://github.com/component/component/wiki/Spec).  The specification includes details on a JSON manifest file, project directory structure, and submission to the registry.

It would be entirely possible to use these repositories alongside jQuery-powered client-side apps.  Quite a few will work well in Node.  I haven't seen many projects using these components yet, but lots of them are worth adding to your GitHub starred repositories.
