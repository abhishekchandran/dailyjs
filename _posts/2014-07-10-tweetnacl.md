---
layout: post
title: "TweetNaCl.js"
author: "Alex Young"
categories:
- cryptography
- modules
- libraries
---

[TweetNaCl.js](http://dchest.github.io/tweetnacl-js/#/) (GitHub: [dchest/tweetnacl-js](https://github.com/dchest/tweetnacl-js), npm: [tweetnacl](https://www.npmjs.org/package/tweetnacl)) is a JavaScript port of [TweetNaCl](http://tweetnacl.cr.yp.to/) -- a cryptography library in 100 tweets.

[NaCl](http://nacl.cr.yp.to/) in this case isn't Google Native Client or sodium chloride, but a library for fast cryptographic operations.  TweetNaCl builds on it to implement an auditable high-security cryptographic library.  There's [a paper on it](http://tweetnacl.cr.yp.to/tweetnacl-20131229.pdf) with more details.

TweetNaCl.js is interesting because it ports all of this to JavaScript, using the new 64-bit `TypedArray` APIs, like `Float64Array`.  It implements secret-key authenticated encryption, public-key authenticated encryption, hashing, and public-key signatures.

One of the authors, Dmitry Chestnykh, said this about the library:

> It's not a toy crypto library: the underlying primitives are djb's (<https://en.wikipedia.org/wiki/Daniel_J._Bernstein>) XSalsa20, Poly1305, Curve25519, and Ed25519, which are used OpenSSH and draft TLS (<http://googleonlinesecurity.blogspot.com/2014/04/speeding-up-and-strengthening-https.html5>).

You can install it with npm or Bower.  As far as usage goes, I've been looking at the code in the tests to get a feel for how it works, but there's documentation in the readme as well:

{% highlight javascript %}
test('nacl.sign and nacl.sign.open specified vectors', function(t) {
  specVectors.forEach(function(vec) {
    var keys = nacl.sign.keyPair.fromSecretKey(dec(vec[0]));
    var msg = dec(vec[1]);
    var goodSig = dec(vec[2]);

    var sig = nacl.sign(msg, keys.secretKey);
    t.equal(enc(sig), enc(goodSig), 'signatures must be equal');
    var openedMsg = nacl.sign.open(msg, sig, keys.publicKey);
    t.equal(enc(openedMsg), enc(msg), 'messages must be equal');
  });
  t.end();
});
{% endhighlight %}

