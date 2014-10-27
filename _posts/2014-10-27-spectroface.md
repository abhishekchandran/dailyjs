---
layout: post
title: "Recreating the Spectrogram Face"
author: "Alex Young"
image: "/images/posts/spectroface.png"
categories:
- audio
- video
- webaudio
---

![Spectroface](/images/posts/spectroface.png)

Enjoying [Syro](https://bleep.com/release/53848-aphex-twin-syro)?  I'll admit I was a little bit too obsessed by the cover art, which contains a list of Aphex Twin's expenses and a list of the audio hardware used on the album.  So I thought it was pretty cool to see [Spectroface](http://danielrapp.github.io/spectroface/) by Daniel Rapp.  This project uses the Web Audio API to recreate Aphex Twin's spectrogram face that was hidden in the [Windowlicker](http://en.wikipedia.org/wiki/Windowlicker) b-side.

Daniel's website explains how spectrograms work, and the [source code](https://github.com/DanielRapp/spectroface/tree/master/src) is heavily commented, so with a little bit of effort you should be able to follow it.

> A spectrogram is a visual representation of the frequencies which make up a sound. Say you whistle a pure "middle C", then a spectrogram would light up right at 261.6 Hz, which is the corresponding frequency for that tone. Likewise, the "A" note makes the spectrogram turn bright white at 440 Hz.

If you hover over "middle C" and "A" on the original page (<http://danielrapp.github.io/spectroface>) it'll actually play the notes, which is a nice touch.
I tried out Daniel's examples and found they work best in Chrome with the webcam and mic active.  You should play the sounds from the speaker rather than headphones to see the image encoding effect in the spectrogram visualisations.

The source is concise, and amazingly doesn't require too much hacking to get the audio values translated into pixels.  For example, the code that determines the shade of grey to use for position x, y in the image looks like this:

{% highlight javascript %}
var getImageDataIntensity = function(imgData, x, y) {
  var r = imgData.data[ ((imgData.width * y) + x) * 4     ]
    , g = imgData.data[ ((imgData.width * y) + x) * 4 + 1 ]
    , b = imgData.data[ ((imgData.width * y) + x) * 4 + 2 ]
    , avg = (r+b+g)/3
    , intensity = avg/255;

  return intensity;
};
{% endhighlight %}

The last example treats the video as an instrument, so you can wave things in front of the camera to produce different sounds.  Although it sounds extremely loud and strange, it's very interesting and comes from a surprisingly small amount of code.

> It starts acting like an instrument! Notice that if you place your finger over the webcam, the sound is muted. You can produce low-pass or high-pass filters by covering only part of the webcam.


