iScroll-native
===============

This is a fork of the excellent [iScroll](http://cubiq.org/iscroll-4) library for a very specific use case.

As of iOS 5, Mobile Safari finally supports native scrolling inside elements with ```overflow: auto```. Thus iScroll is no longer necessary just to get scrolling divs in iDevices.

However, Mobile Safari's native inertial scrolling pauses all DOM updates and fires no JS events *during* scrolling. This is problematic for advanced scrolling effects like sticky elements that anchor to the viewport when scrolled past. With native scrolling, the page contents will freeze until scrolling comes to a complete stop, and only then will any DOM changes jump into place.

iScroll solves this nicely. By replacing native scrolling, you can fire events continuously while the user's finger is in motion. But it does this by manipulating the top/left or transform properties. This leaves tworemaining problems for advanced effects:

1. It's incompatible with other scroll-based libraries, e.g. [jQuery Waypoints](http://imakewebthings.com/jquery-waypoints/).

2. The default transform-based scrolling [breaks position:fixed elements](http://meyerweb.com/eric/thoughts/2011/09/12/un-fixing-fixed-elements-with-css-transforms/). (Using the fallback top/left scrolling solves this, but at the cost of smooth scrolling on older iDevices.)

iScroll-native fixes this by adding a ```useNativeScroll``` option. When this is set to true, the ```scrollTop``` and ```scrollLeft``` properties of the wrapper element will be used instead of css transforms or top/left properties on the scrolling content, and the wrapper will be set to ```overflow: auto``` instead of ```overflow: hidden```. Example usage:

```
var myScroll = new iScroll('wrapper_id', {
	useNativeScroll: true
});
```

This gets you a scrolling element that:

* Works on desktop and mobile browsers.

* Preserves native scrollbars -- no need to fake it.

* Is compatible with other scrolling libraries and event handlers.

* Is compatible with native scrolling, e.g. if a desktop user actually clicks a native scrollbar button.

* As a bonus for desktop browsers, also prevents [fixed position elements swallowing mousewheel events](http://stackoverflow.com/questions/7182502/pass-mousewheel-event-through-fixed-content).


Disclaimer of hackiness
===============

I forked this specifically for my own project that needed sticky elements on vertical scrolling with iPad and desktop support. I haven't tested it for anything else. If you have other uses in mind, I strongly encourage you to check out the original [iScroll](http://cubiq.org/iscroll-4) first, and if that's not enough use iScroll-native as a guide for your own modifications. iScroll is a solid, tested, deployable solution to several problems. iScroll-native is a quick hack. :)


License
===============

Copyright (c) 2012 Matteo Spinelli, http://cubiq.org/

Modified from original source 2013 Nick B-W (@pseudomammal)

Permission is hereby granted, free of charge, to any person
obtaining a copy of this software and associated documentation
files (the "Software"), to deal in the Software without
restriction, including without limitation the rights to use,
copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the
Software is furnished to do so, subject to the following
conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES
OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT
HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY,
WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING
FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR
OTHER DEALINGS IN THE SOFTWARE.