CSS Only Mustard Cut
====================

Cutting the Mustard without Javascript. Also known as CSSCTM (CSS Cut-the-Mustard).

Read the [SitePoint article](http://www.sitepoint.com/cutting-the-mustard-with-css-media-queries/).

I hope to keep this repo up to date with any new 'cuts' or related techniques as and when they're developed or suggested.

Please raise issues for any problems, ideas or 'cuts'.

~AK


The Original Cut
----------------
~~~html
<!--
    IE 9+, FF 8+, Opera 12, Chrome 29+, Android ~4.4+
    Chrome 29+, Opera 16+, Safari 6.1+, iOS 7+, Android ~4.4+
-->
<link rel="stylesheet" href="your-stylesheet.css" media="
    only screen and (min-resolution: 0.1dpcm),
    only screen and (-webkit-min-device-pixel-ratio:0) and (min-color-index:0)
">
~~~

[Test page](http://fall-back.github.io/test/support.html)

Edge fails with the line breaks in place. **Remove line breaks in production.**


The M3 Cut (Much More Modern)
-----------------------------

~~~html
<!--
    Print (Edge doesn't apply to print otherwise)
    IE 10, 11
    Edge
    Chrome 29+, Opera 16+, Safari 6.1+, iOS 7+, Android ~4.4+
    FF 29+
-->
<link rel="stylesheet" href="your-stylesheet.css" media="
    only print, screen and (min-width: 1vm),
    only all and (-ms-high-contrast: none), only all and (-ms-high-contrast: active),
    only all and (pointer: fine), only all and (pointer: coarse), only all and (pointer: none),
    only all and (-webkit-min-device-pixel-ratio:0) and (min-color-index:0),
    only all and (min--moz-device-pixel-ratio:0) and (min-resolution: 3e1dpcm)
">
~~~

[Can I Use](http://caniuse.com/#compare=ie+10,firefox+29,chrome+29,safari+6.1,opera+16,ios_saf+7.0-7.1,android+4.4) (Yay, Flexbox!)

[Test page](http://fall-back.github.io/test/support-m3.html)

To remove IE 10 and 11 support, remove the 2nd line (`only all and (-ms-high-contrast: none), only all and (-ms-high-contrast: active),`).

<s>Note that if you're combining the links media queries into one I tried putting in line breaks to make it more readable, but this cause IE9 to ignore the query and apply the styles, so DON'T ADD LINE BREAKS.</s>
 - For some reason I can't recreate the above. Something else may have been the cause of this problem.
 

M3+9
----

I recently descovered that the Edge print fix for the M3 cut actually let IE9 through, so if you need IE9+ support (instead of 10+), then use this:

~~~html
<!--
    Print (Edge doesn't apply to print otherwise), IE9
    IE 10, 11
    Edge
    Chrome 29+, Opera 16+, Safari 6.1+, iOS 7+, Android ~4.4+
    FF 29+
-->
<link rel="stylesheet" href="your-stylesheet.css" media="
    only print,
    only all and (-ms-high-contrast: none), only all and (-ms-high-contrast: active),
    only all and (pointer: fine), only all and (pointer: coarse), only all and (pointer: none),
    only all and (-webkit-min-device-pixel-ratio:0) and (min-color-index:0),
    only all and (min--moz-device-pixel-ratio:0) and (min-resolution: 3e1dpcm)
">
~~~


The EM2 Cut (Even More Modern)
------------------------------

~~~html
<!--
    Print (Edge doesn't apply to print otherwise)
    Edge, Chrome 39+, Opera 26+, Safari 9+, iOS 9+, Android ~5+, Android UCBrowser ~11.8+
    FF 47+
-->
<link rel="stylesheet" href="your-stylesheet.css" media="
    only print,
    only all and (pointer: fine), only all and (pointer: coarse), only all and (pointer: none),
    only all and (min--moz-device-pixel-ratio:0) and (display-mode:browser), (min--moz-device-pixel-ratio:0) and (display-mode:fullscreen)
">
~~~

[Can I Use](https://caniuse.com/#compare=edge+12,firefox+47,chrome+39,safari+9,opera+26,ios_saf+9.0-9.2,android+62)

[Test page](http://fall-back.github.io/test/support-em2.html)

Note that:
* Android ~5+ is according to caniuse, though it works on ~4.3+ if using Chrome or Samsung
* Android UCBrowser 11.8+ is according to caniuse though currently untested. Does not work on Android UCBrowser 11.3.2

---

Note the Android versions aren't certain because it actually depends on the WebKit version that's being used. For example, I've seen the styles actually work on an Android 4.3 device (emulated) because it was using a modern enough version of WebKit. So far, I've been unable to determine at exactly which version support starts but it appears to be somewhere between 535.19 and 537.36. It's complicated.

---


Mix and Match
-------------

For clarity, you can mix and match the queries for more customised support.

Print
~~~css
only print
~~~
---

IE 9+, FF 8+, Opera 12, Chrome 29+, Android ~4.4+
~~~css
only screen and (min-resolution: 0.1dpcm)
~~~
---

IE 10, 11
~~~css
only all and (-ms-high-contrast: none), only all and (-ms-high-contrast: active)
~~~
---

Chrome 29+, Opera 16+, Safari 6.1+, iOS 7+, Android ~4.4+
~~~css
only screen and (-webkit-min-device-pixel-ratio:0) and (min-color-index:0)
~~~
---

Edge, Chrome 39+, Opera 26+, Safari 9+, iOS 9+, Android ~5+*, Android UCBrowser 11.8+**

[*]  (according to caniuse, though it works on ~4.3+ if using Chrome or Samsung)

[**] (according to caniuse though currently untested. Does not work on Android UCBrowser 11.3.2)
~~~css
only all and (pointer: fine), only all and (pointer: coarse), only all and (pointer: none)
~~~
---

FF 29+
~~~css
only all and (min--moz-device-pixel-ratio:0) and (min-resolution: 3e1dpcm)
~~~
---

FF 47+
~~~css
only all and (min--moz-device-pixel-ratio:0) and (display-mode:browser), (min--moz-device-pixel-ratio:0) and (display-mode:fullscreen)
~~~
---

UCBrowser (JS user-agent sniff*)
~~~javascript
if (navigator.userAgent.indexOf('UCBrowser') > -1) {
  var link  = document.createElement('link');
  link.rel  = 'stylesheet';
  link.href = 'your-stylesheet.css';
  document.getElementsByTagName('head')[0].appendChild(link);
  // You may also want to add a class to be able to target these browsers in CSS:
  document.getElementsByTagName('html')[0].className += ' ucbrowser';
}
~~~

Opera Mini (JS user-agent sniff*)
~~~javascript
if (navigator.userAgent.indexOf('Opera Mini') > -1 || navigator.userAgent.indexOf('OPiOS') > -1) {
  var link  = document.createElement('link');
  link.rel  = 'stylesheet';
  link.href = 'your-stylesheet.css';
  document.getElementsByTagName('head')[0].appendChild(link);
}
~~~

[*] So far as I'm aware it's not possible to disable JS in UCBrowser or Opera Mini, so if the 'sniffs' are placed in HTML rather than an external file, things aren't likely to go wrong.

---

IE8 (uses conditional comments)
~~~html
<!--[if IE 8]>
<link rel="stylesheet" href="your-stylesheet.css">
<![endif]-->
~~~


Mentions
--------

* https://alistapart.com/article/the-slow-death-of-internet-explorer-and-future-of-progressive-enhancement
* https://www.smashingmagazine.com/2019/03/web-on-internet-explorer-ie8/


Usage
-----

* https://github.com/springernature/frontend-playbook/blob/master/practices/graded-browser-support.md
