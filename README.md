CSS Only Mustard Cut
====================

Cutting the Mustard without Javascript.

Read the SitePoint article: http://www.sitepoint.com/cutting-the-mustard-with-css-media-queries/

I hope to keep this repo up to date with any new 'cuts' or related techniques as and when they're developed or suggested.

Please raise issues for any problems, ideas or 'cuts'.

~AK


The Original Cut
----------------
~~~
<!-- IE 9+, FF 8+, Opera 12, Chrome 29+, Android ~4.4+ -->
<link rel="stylesheet" href="css/your-stylesheet.css"
  media="only screen and (min-resolution: 0.1dpcm)">
<!-- Chrome 29+, Opera 16+, Safari 6.1+, iOS 7+, Android ~4.4+ -->
<link rel="stylesheet" href="css/your-stylesheet.css"
  media="only screen and (-webkit-min-device-pixel-ratio:0) and (min-color-index:0)">
~~~

[Test page](http://fall-back.github.io/test/support.html)

The M3 Cut (Much More Modern)
-----------------------------

~~~
<!-- Chrome 29+, Opera 16+, Safari 6.1+, iOS 7+, Android ~4.4+, IE10+ (including Edge) -->
<link rel="stylesheet" href="css/your-stylesheet.css"
  media="only screen and (-webkit-min-device-pixel-ratio:0) and (min-color-index:0), (-ms-high-contrast: none)">
<!-- FF29+ -->
<link rel="stylesheet" href="css/your-stylesheet.css"
  media="only all and (min--moz-device-pixel-ratio:0) and (min-resolution: 3e1dpcm)">
~~~

[Can I Use](http://caniuse.com/#compare=ie+10,firefox+29,chrome+29,safari+6.1,opera+16,ios_saf+7.0-7.1,android+4.4) (Yay, Flexbox!)

[Test page](http://fall-back.github.io/test/support-m3.html)

---

Note the Android versions aren't certain because it actually depends on the WebKit version that's being used. For example, I've seen the styles actually work on an Android 4.3 device (emulated) because it was using a modern enough version of WebKit. So far, I've been unable to determine at exactly which version support starts but it appears to be somewhere between 535.19 and 537.36. It's complicated.
