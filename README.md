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

I recently discovered that the Edge print fix for the M3 cut actually let IE9 through, so if you need IE9+ support (instead of 10+), then use this:

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

TNG Cut (The Next Generation)
-----------------------------

~~~html
<!--
    Print, Edge 12? - 18
    Edge 79+, Chrome 58+, Opera 45+, Safari 10+, iOS 10+, Android Webview/Chrome 58+, Samsung Internet
    FF 47+
-->
<link rel="stylesheet" href="your-stylesheet.css" media="
    only print, screen and (min-width: 1vm),
    only all and (color-gamut: srgb), only all and (color-gamut: p3), only all and (color-gamut: rec2020),
    only all and (min--moz-device-pixel-ratio:0) and (display-mode:browser), (min--moz-device-pixel-ratio:0) and (display-mode:fullscreen)
">
~~~

---

PRM Cut (Prefers Reduced Motion)
-----------------------------

~~~html
<!--
    Print (Edge doesn't apply to print otherwise)
    Edge 79+, Chrome 74+, Firefox 63+, Opera 64+, Safari 10.1+, iOS 10.3+, Android 81+
-->
<link rel="stylesheet" href="your-stylesheet.css" media="
    only print,
    only all and (prefers-reduced-motion: no-preference), only all and (prefers-reduced-motion: reduce)
">
~~~

[Can I Use](https://caniuse.com/?compare=edge+79,firefox+63,chrome+74,safari+10.1,opera+64,ios_saf+10.3,android+81,and_chr+89,and_ff+86,samsung+11.1-11.2)

[Test page](http://fall-back.github.io/test/support-prm.html)

---

PCS Cut (Prefers Color Scheme)
-----------------------------

~~~html
<!--
    Print (Edge doesn't apply to print otherwise)
    Edge 79+, Chrome 76+, Firefox 67+, Opera 62+, Safari 12.1+, iOS 13+, Android 91+
-->
<link rel="stylesheet" href="mq-test.css" media="
    only print,
    only all and (prefers-color-scheme: no-preference),
    only all and (prefers-color-scheme: light),
    only all and (prefers-color-scheme: dark)
">
~~~

[Can I Use](https://caniuse.com/?compare=edge+79,firefox+63,chrome+74,safari+10.1,opera+64,ios_saf+10.3,android+81,and_chr+89,and_ff+86,samsung+11.1-11.2&compareCats=CSS)

[Test page](http://fall-back.github.io/test/support-pcs.html)

---

PC Cut (Prefers Contrast)
-----------------------------

~~~html
<!--
    Print (Edge doesn't apply to print otherwise)
    Edge 79+, Chrome 76+, Firefox 67+, Opera 62+, Safari 12.1+, iOS 13+, Android 91+
-->
<link rel="stylesheet" href="mq-test.css" media="
    only print,
    only all and (prefers-contrast: no-preference),
    only all and (prefers-contrast: more),
    only all and (prefers-contrast: less),
    only all and (prefers-contrast: custom)
">
~~~

[Can I Use](https://caniuse.com/?compare=chrome+96,edge+96,safari+14.1,firefox+101,opera+82,and_chr+119,ios_saf+14.5-14.8,samsung+17.0,android+119,and_ff+119&compareCats=CSS)

[Test page](http://fall-back.github.io/test/support-ps.html)

Note I've been unable to verify the cut-off for Android as BrowserStack devices all work despite reported browser versions.

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


---

Other Techniques
----------------

### TLS

All websites should by now be serving the pages over https. A security certificate is crucial in the modern age, but older browser do not support TLS and will refuse to load the page.
This can be considered a natural 'cut' and can be factored in to your fallback support strategy without having to add any extra code.

[TLS 1.1](https://caniuse.com/tls1-1) is deprecated so shouldn't really be used, but [TLS 1.2](https://caniuse.com/tls1-2) and [TLS 1.3](https://caniuse.com/tls1-3) are stilll current (at time of writing) so if you're serving your site over these, use the CSS support tables as your starting point for your CSS 'cut'. You may find it's the only 'cut' you need.


### Feature Queries

Whilst it should be common practice to wrap bleeding-edge CSS in `@supports` blocks and provide sensible fallbacks for non-supporting browsers, it's possible to wrap your *entire* CSS in one, to bump up the baseline of browsers you're supporting. So for example if your layouts rely heavily on CSS subgrid and everything else is more widely supported, you can wrap all your CSS in a block like this:

```
@supports (grid-template-columns: subgrid) {
    /* all your CSS here */
}
```

Then [non-supporting](https://caniuse.com/css-subgrid) (older) browsers will be cut and you won't have to worry about them looking all broken (so long as you've followed the FallBack Philosophy and coded your HTML nicely (properly)).
