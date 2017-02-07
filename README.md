CSS Only Mustard Cut
====================

Cutting the Mustard without Javascript.

Read the [SitePoint article](http://www.sitepoint.com/cutting-the-mustard-with-css-media-queries/).

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
<!--
    Print (Edge doesn't apply to print otherwise)
    Edge
    IE 10, 11
    Chrome 29+, Opera 16+, Safari 6.1+, iOS 7+, Android ~4.4+
    FF29+   
-->
<link rel="stylesheet" href="css/mq-test.css" media="
    only print,
    only all and (-ms-high-contrast: none), only all and (-ms-high-contrast: active),
    only all and (pointer: fine), only all and (pointer: coarse), only all and (pointer: none),
    only all and (-webkit-min-device-pixel-ratio:0) and (min-color-index:0),
    only all and (min--moz-device-pixel-ratio:0) and (min-resolution: 3e1dpcm)
">
~~~

[Can I Use](http://caniuse.com/#compare=ie+10,firefox+29,chrome+29,safari+6.1,opera+16,ios_saf+7.0-7.1,android+4.4) (Yay, Flexbox!)

[Test page](http://fall-back.github.io/test/support-m3.html)

<s>Note that if you're combining the links media queries into one I tried putting in line breaks to make it more readable, but this cause IE9 to ignore the query and apply the styles, so DON'T ADD LINE BREAKS.</s>
 - For some reason I can't recreate the above. Something else may have been the cause of this problem.

---

Note the Android versions aren't certain because it actually depends on the WebKit version that's being used. For example, I've seen the styles actually work on an Android 4.3 device (emulated) because it was using a modern enough version of WebKit. So far, I've been unable to determine at exactly which version support starts but it appears to be somewhere between 535.19 and 537.36. It's complicated.
