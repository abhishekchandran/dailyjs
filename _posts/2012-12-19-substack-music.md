---
layout: post
title: "Substack's Musical Node Modules"
author: "Alex Young"
categories: 
- node
- modules
- audio
- music
---

<div class="intro">
<strong>Prerequisites</strong>: Install <a href="http://www.gnuplot.info/">gnuplot</a> and <a href="http://sox.sourceforge.net/">SoX</a> to follow along.
</div>

James Halliday, otherwise known as "substack", has been making what he calls [computer generated beepstep](https://soundcloud.com/substack/beepstep) using two new modules: [baudio](https://github.com/substack/baudio) (npm: [baudio](https://npmjs.org/package/baudio), License: _MIT_) and [plucky](https://github.com/substack/plucky) (npm: [plucky](https://npmjs.org/package/plucky), License: _MIT_).

The baudio module returns a [readable stream](http://nodejs.org/docs/latest/api/all.html#all_readable_stream) that generates raw audio data.  It requires [SoX](http://sox.sourceforge.net/) to play or record audio, which should be installable from your package manager (Debian has it, and so does [Homebrew](http://mxcl.github.com/homebrew/)).

The callback passed to the `baudio` function receives two arguments: `t` and `i` -- the time in seconds, and a counter.  The callback will be run using `process.nextTick` to generate a stream of audio data.  The audio data will be passed to SoX for playback or recording using [child_process.spawn](http://nodejs.org/docs/latest/api/all.html#all_child_process_spawn_command_args_options).

The audio data itself is where things get interesting.  The baudio stream is sent directly into SoX through SoX's "pipeline" mode, in which audio data is read from standard input, using the "s16" format -- it's streams all the way down!  Internally, baudio converts the float values returned from the callback into integers, which are written to a buffer using Node's [buf.writeInt16LE](http://nodejs.org/docs/latest/api/all.html#all_buf_writeint16le_value_offset_noassert) method.

Your callback should generate floating point values between `-1.0` and `1.0`.  By default, baudio is set to use a frequency of 44 kHz -- that's 44,000 values a second.  This is close to CD quality (44.1 kHz).

Unless you're well-versed in audio programming, generating sounds with baudio is going to be hard work.  To help you understand what's going on, I've written a small example that uses gnuplot to visualise the output.

First, install baudio:

{% highlight text %}
npm install baudio
{% endhighlight %}

And then create a file called `baudio-simple.js`:

{% highlight javascript %}
var baudio = require('baudio')
  , out = process.stdout
  , note = 1.0
  ;

var b = baudio(function(t, i) {
  var value = Math.sin(Math.PI * t * 261.626);
  out.write(value.toString() + '\n');
  return value;
});

setTimeout(function() {
  b.end();
}, 1000);

b.play();
{% endhighlight %}

This file can be run with `node baudio-simple.js > audio.dat` (the redirection is important for generating the graphs), and if you've got SoX installed you'll get a sound.

Now you're going to write a bit of gnuplot.  Create a file called `baudio-plot` with this script:

{% highlight text %}
#!/usr/bin/env gnuplot

set terminal png size 530,420
set output "baudio.png"
plot "audio.dat" using 0:1 with lines
{% endhighlight %}

Now make it executable, and run it:

{% highlight text %}
chmod 700 baudio-plot
./baudio-plot
{% endhighlight %}

It should generate a file called `baudio.png` with a second's worth of audio data plotted.

<div class="image">
  <img src="/images/posts/baudio-1.png" alt="" />
  <small>A graph of baudio's output using one second of audio.</small>
</div>

If you're looking at `Math.sin` in the example code and wondering why there isn't a beautiful sweeping sine wave, then the reason is simple: there's too much data.  Let's try ending the output earlier:

{% highlight javascript %}
var baudio = require('baudio')
  , out = process.stdout
  , note = 1.0
  ;

var b = baudio(function(t, i) {
  if (i > 100) b.end();
  var value = Math.sin(Math.PI * t * 261.626);
  out.write(value.toString() + '\n');
  return value;
});

b.play();
{% endhighlight %}

Now your graph should look like a wave, but you won't hear much sound:

<div class="image">
  <img src="/images/posts/baudio-short.png" alt="" />
  <small>A much shorter sample shows the output really is a sine wave.</small>
</div>

###Wave Period and Amplitude

The simple example I've used above is focused on controlling the "wave period", or the pitch of the output.  To demonstrate this, try changing `261.626` to `60.0`:

<div class="image">
  <img src="/images/posts/baudio-bass.png" alt="" />
  <small>Some sub-bass.</small>
</div>

Now the output is a lower pitch, and the graph makes this clear because you can see there are less cycles in the same amount of time.  So we've mastered pitch, but what about volume?

It's actually easy once you know what the wave equation is doing.  The generalised equation is `A sin(t - K) + b` (from [Amplitude on Wikipedia](http://en.wikipedia.org/wiki/Amplitude)).  In programmer-speak, this equation can be written as `A * sin(t - K) + b`, where `A` is the "peak amplitude of the wave", `t` is time (which we already know baudio gives us), and `K` and `b` are offsets for the wave (which I'm not going to talk about here).

That gives rise to the following example that allows volume to be controlled by adding a variable, `vol`, for `A`:

{% highlight javascript %}
var baudio = require('baudio')
  , out = process.stdout
  , note = 1.0
  , vol = 0.1
  ;

var b = baudio(function(t, i) {
  if (i > 100) b.end();
  var value = vol * Math.sin(Math.PI * t * 261.626);
  out.write(value.toString() + '\n');
  return value;
});

b.play();
{% endhighlight %}

The graph is now appropriately smaller:

<div class="image">
  <img src="/images/posts/baudio-quiet.png" alt="" />
  <small>A quieter audio sample, plotted with <code>set yrange [-1.0:1.0]</code> to correct the axis.</small>
</div>

###More Fun Stuff

If you've managed to get gnuplot and SoX installed and played around with these examples, then there's more!  First, try taking a look at [plucky](https://github.com/substack/plucky), which can be used to make "arrangements" of callbacks that generate different channels of audio.  Also, James wrote [beepstep.js](https://gist.github.com/4325336) which is a much more involved example than anything I've talked about here.

And, James tweets about this stuff, so follow [@substack](http://twitter.com/substack) if you're into streams and audio hacking.

