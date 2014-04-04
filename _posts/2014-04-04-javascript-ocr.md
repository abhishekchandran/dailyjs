---
layout: post
title: "JavaScript OCR"
author: "Alex Young"
categories:
- ocr
- libraries
- emscripten
---

<div class="image">
  <img src="/images/posts/jsocr.png" />
  <small>What should happen.</small>
</div>

Konrad Dzwinel sent in a [JavaScript OCR demo](http://kdzwinel.github.io/JS-OCR-demo/).  It uses getUserMedia to get images from the camera, glfx.js and JCrop for user-driven image correction, and [ocrad.js](https://github.com/antimatter15/ocrad.js/) to handle the character recognition.

The [Ocrad.js demo](http://antimatter15.github.io/ocrad.js/demo.html) managed to recognise the text in my sample image.  I noticed it didn't work with white on black text -- it had to be inverted for the correct text to be recognised.

<div class="image">
  <img src="/images/posts/heroocrad.png" />
  <small>Ocrad.js</small>
</div>

Ocrad.js is an Emscripten-based translation of [Ocrad](http://www.gnu.org/software/ocrad/ocrad.html) by Antonio Diaz Diaz.  Kevin Kwok, who put together Ocrad.js, also ported GOCR to JavaScript with Emscripten as [gocr.js](https://github.com/antimatter15/gocr.js).

[GOCR](http://jocr.sourceforge.net/) was started by Joerg Schulenburg, but has had other contributors since the original release back in 2000.  Kevin compares both libraries and his experiences getting them running in JavaScript:

> Anyway, I tried to compile GOCR first and was immediately struck by how easy and painless it had been. I was on a roll, and decided to do Ocrad as well. It wasn't particularly hard- sure it was slightly more involved but still hardly anything.

He also mentions Tesseract, which is a popular OCR system but also widely known to be very large:

> In fact, what's absolutely stunning is the sheer universality of Tesseract. Just about everything which claims to have text recognition as a feature is backed by it. At one point, I was hoping that Mathematica had some clever routine using morphology and symbolic new kinds of sciences and evolved automata pattern recognition. Nope! Nestled deep within the gigabytes of code lies the Chuck Testa of textadermies: Tesseract.

I thought Konrad's demo was cool -- being able to edit the brightness, contrast, and crop the image was a nice use of client-side technology.  However, so far I've had the problem Kevin mentioned: occasional blocks of nothing, or seemingly random text, then suddenly excellent results.
