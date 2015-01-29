---
layout: post
title: "Deploy Apps with Flightplan"
author: Alex Young
categories:
- node
- modules
- libraries
- deployment
---

If you saw my post about Shipit yesterday, then you might be interested in trying out Patrick Stadler's module, Flightplan (GitHub: [pstadler/flightplan](https://github.com/pstadler/flightplan), License: _MIT_, npm: [flightplan](https://www.npmjs.com/package/flightplan)).  Flightplan is a deployment library that is more influenced by [Python's Fabric](http://www.fabfile.org/) than Ruby's Capistrano.  It can also be used for general administration tasks as well.

If you want to use it, you'll need a `flightplan.js` file.  This defines the deployment targets, like staging and production, and contains the local and remote commands to run.  I like the syntax of the plans because they're based on simple JavaScript callbacks with locally scoped variables rather than any kind of magic globals:

{% highlight javascript %}
plan.remote(function(remote) {
  remote.log('Move folder to web root');
  remote.sudo('cp -R /tmp/' + tmpDir + ' ~', {user: 'www'});
  remote.rm('-rf /tmp/' + tmpDir);

  remote.log('Install dependencies');
  remote.sudo('npm --production --prefix ~/' + tmpDir
                            + ' install ~/' + tmpDir, {user: 'www'});

  remote.log('Reload application');
  remote.sudo('ln -snf ~/' + tmpDir + ' ~/example-com', {user: 'www'});
  remote.sudo('pm2 reload example-com', {user: 'www'});
});
{% endhighlight %}

Groups of commands like this are called "flights".  You can run subsets of flights, which are known as tasks:

{% highlight javascript %}
plan.local(['deploy', 'build'], function(transport) {});
plan.remote(['deploy', 'build'], function(transport) {});
{% endhighlight %}

The `transport` argument for flights contains a `runtime` property that lets you query the target, hosts, and options.  You could use this to print extra debugging information based on options passed to the task.  This design means you could split flights into separate modules, which might be useful if you need to orchestrate the deployment of a collection of separate apps or microservices.

Transports also have some handy utility methods.  You can rsync files with the `transfer` method, like this: `local.transfer(['file.txt', '/tmp/foo')`.  If you want to ask questions during a script you can use `transport.prompt` -- this might be useful for restricting deployment to specific employees without having to store passwords in your repository.  There's also a `waitFor` method that can be used to wrap asynchronous operations.

The fact it supports synchronous, blocking operations means you can write lists of commands more like the way shell scripts operate.  I assume this is how most devops and sysadmins prefer to work, so Flightplan might make more sense to them rather than dealing with asynchronous APIs.

To make this possible Flightplan uses [fibers](https://www.npmjs.com/package/fibers).  Here's a snippet from [lib/flight/remote.js](https://github.com/pstadler/flightplan/blob/master/lib/flight/remote.js):

{% highlight javascript %}
var execute = function(transport) {
  var future = new Future();
  new Fiber(function() {
    var t = process.hrtime();
    logger.info('Executing remote task on ' + transport.runtime.host);
    fn(transport);
    logger.info('Remote task on ' + transport.runtime.host +
                ' finished after ' + prettyTime(process.hrtime(t)));
    return future.return();
  }).run();
  return future;
};
{% endhighlight %}

Patrick notes that Flightplan now supports cloud providers (including EC2 on Amazon and DigitalOcean), so you can easily define the remote hosts which may change with large projects on such services.  In a way I think this makes Flightplan a little bit like Puppet and Chef.  If you still haven't found your perfect deployment solution, or if you have to maintain remote servers, then you should give it a try.

