---
layout: post
title: "Node Roundup: Who's Hiring, Melkor, Isosurface"
author: "Alex Young"
categories:
- node
- modules
- npm
- jobs
- graphics
- es6
- generators
---

###npm: Who's Hiring?

I noticed npm's blog had a post about [who's hiring in the Node community](http://blog.npmjs.org/post/84177685575/whos-hiring-node-js-developers).  There's a new [Who's Hiring](https://www.npmjs.org/whoshiring) page on npmjs.org, that lists Voxer, The Financial Times, Branding Brand, and Dash.

###Melkor

More people are getting interested in [Koa.js](http://koajs.com/) now, so it's good to start collecting example applications that use it.  Ramesh Nair sent in [Melkor](https://github.com/hiddentao/melkor) (License: _MIT_), a wiki that uses [Waigo](https://www.npmjs.org/package/waigo) which is built on Koa.js, and Git as the storage system.

You can see generators used right away in `index.js`:

{% highlight javascript %}
exports.init = function*(folder, options) {
  debug('Folder: ' + folder);

  yield* waigo.init({
    appFolder: path.join(__dirname, 'src')
  });

  var App = waigo.load('application');

  yield* App.start({
    postConfig: function(config) {
      config.startupSteps.unshift('wiki');

      config.middleware.push({ id: 'methodOverride' });

      debug('Port: ' + config.port);
      config.port = options.port;
      config.baseURL = 'http://localhost:' + config.port;

      config.staticResources.folder = '../public/build';

      config.wikiTitle = options.title;
      config.wikiFolder = folder;
    }
  });

  return App;
};
{% endhighlight %}

The controllers also make heavy use of `yield`, so things like form validation and template rendering have a synchronous feel.

###Isosurface

![Isosurface](/images/posts/isosurface.png)

[Isosurface](http://mikolalysenko.github.io/Isosurface/) (GitHub: [mikolalysenko / isosurface](https://github.com/mikolalysenko/isosurface), License: _MIT_, npm: [isosurface](https://www.npmjs.org/package/isosurface)) by Mikola Lysenko is a set of isosurface polygonizer algorithms.

Here's an example:

{% highlight javascript %}
var isosurface = require('isosurface');

var mesh = isosurface.surfaceNets([64,64,64], function(x,y,z) {
  return x*x + y*y + z*z - 100;
}, [[-11,-11,-11], [11,11,11]]);
{% endhighlight %}

I found this module (and the impressive demo) while looking through Mikola's graphics related modules on [npmjs.org/~mikolalysenko](https://www.npmjs.org/~mikolalysenko).
