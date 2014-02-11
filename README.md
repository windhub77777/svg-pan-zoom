svg-pan-zoom library
==========================

JavaScript library that enables panning and zooming of an SVG in an HTML document, including SVGs in HTML 'object' or 'embed' elements and in-line SVGs. The library responds to mouse events and offers hooks for custom, programmatic control of pan and zoom behavior.

Capabilities:
  * Pan with mouse events or custom JavaScript hooks
  * Zoom with mouse events (wheel or double-click) or custom JavaScript hooks
  * Element dragging with mouse events (custom JavaScript hooks not provided, but if you need them, check out [D3.js](http://d3js.org/))

Demo
----
 Pan and zoom the SVG tiger on [github pages](http://ariutta.github.io/svg-pan-zoom/).

How To Use
----------

1) Ensure the target SVG has a top-level 'g' element with the id 'viewport' to enable zooming for the entire SVG:

```xml
<g id="viewport"></g>
```

If the target SVG does not have this element, the library will use the first 'g' element found.

2) Reference the [svg-pan-zoom.js file](http://ariutta.github.io/svg-pan-zoom/svg-pan-zoom.js) from your HTML document and call the init method:

```js
svgPanZoom.init();
```

If you want to override the defaults, you can optionally specify one or more arguments:


```js
svgPanZoom.init({
  'selector': '#my-svg',
  'panEnabled': true, 
  'zoomEnabled': true,
  'dragEnabled': false,
  'zoomScaleSensitivity': 0.2,
  'minZoom': 0.5,
  'maxZoom': 10,
  'onZoom': function(scale) { ... }  // Callback function when zoom changes.
});
```

If any arguments are specified, they must have the following value types:
* 'selector' must be a [CSS selector](http://www.w3.org/TR/CSS2/selector.html). If left blank, svg-pan-zoom will look for the first SVG document in your HTML document.
* 'panEnabled' must be true or false. Default is true.
* 'zoomEnabled' must be true or false. Default is true.
* 'dragEnabled' must be true or false. Default is false.
* 'zoomScaleSensitivity' must be a scalar. Default is 0.2.
* 'minZoom' must be a scalar. Default is 0.5.
* 'maxZoom' must be a scalar. Default is 10.
* 'onZoom' must be a callback function to be called when zoom changes.


To programmatically pan, call the pan method with a direction of 'up', 'down', 'right' or 'left'.

```js
svgPanZoom.pan([selector], direction); // selector is optional.
```

To programmatically zoom, you can use the zoom method to specify your desired scale value:

```js
svgPanZoom.zoom({
  'selector': '#my-svg', // selector is optional
  'scale': 2 // required. values must be scalar.
});
```

Or you can use the zoomIn or zoomOut methods:

```
svgPanZoom.zoomIn([selector]); // selector is optional

svgPanZoom.zoomOut([selector]); // selector is optional

svgPanZoom.resetZoom([selector]); // selector is optional.
```

If you want faster or slower zooming, you can override the default zoom increment with the setZoomScaleSensitivity method.

To programmatically enable/disable pan, zoom or drag:

```js
svgPanZoom.enablePan();
svgPanZoom.disablePan();

svgPanZoom.enableZoom();
svgPanZoom.disableZoom();

svgPanZoom.enableDrag();
svgPanZoom.disableDrag();
```

You can configure the default enabled/disabled state of pan/zoom/drag with the variables listed in the CONFIGURATION section of the file.

Known issues
------------
  * Mouse zoom does not work at all with IE, and pan does not work correctly. See [Issue #21](https://github.com/ariutta/svg-pan-zoom/issues/21).
  * Programmatical Zoom does not zoom on center. See [Issue #4](https://github.com/ariutta/svg-pan-zoom/issues/4).
  * Zooming (while panning) on Safari has still some issues. See [Issue #15](https://github.com/ariutta/svg-pan-zoom/issues/15).

Related Work
------------
This library is based on the [SVGPan](https://code.google.com/p/svgpan/) library. SVGPan is intended for use with the [SVG 'script' element](http://www.w3.org/TR/SVG/script.html), whereas svg-pan-zoom is intended for use with the [HTML 'script' element](http://www.w3.org/TR/html401/interact/scripts.html).

  * 1.3.2), Thu Dec 5 2013, Anders Riutta
    * Addressed issue of overwriting existing viewport transform
    * Added capability to handle SVG documents in object elements
 
  * 1.3.1), Mon Nov 19 2013, Anders Riutta
    * Added programmatic control for pan and zoom 
    * Changed certain terms to make them more intuitive

  * 1.3.0), Mon Nov 18 2013, Anders Riutta
    * Added programmatic control for zoom/pan enabled/disabled

  * 1.2.2) Tue Aug 30 17:21:56 CEST 2011, Andrea Leofreddi
    * Fixed viewBox on svg tag (#7)
    * Improved zoom speed (#2)

  * 1.2.1) Mon Jul  4 00:33:18 CEST 2011, Andrea Leofreddi
    * Fixed a regression with mouse wheel (now working on Firefox 5)
    * Working with viewBox attribute (#4)
    * Added 'use strict;' and fixed resulting warnings (#5)
    * Added configuration variables, dragging is disabled by default (#3)

  * 1.2) Sat Mar 20 08:42:50 GMT 2010, Zeng Xiaohui
    * Fixed a bug with browser mouse handler interaction

  * 1.1) Wed Feb  3 17:39:33 GMT 2010, Zeng Xiaohui
    * Updated the zoom code to support the mouse wheel on Safari/Chrome

  * 1.0) Andrea Leofreddi
    * First release

License
-------
 This code is licensed under the following BSD license:

 ```
 Copyright 2009-2010 Andrea Leofreddi <a.leofreddi@itcharm.com>. All rights reserved.
 
 Redistribution and use in source and binary forms, with or without modification, are
 permitted provided that the following conditions are met:
 
    1. Redistributions of source code must retain the above copyright notice, this list of
       conditions and the following disclaimer.
 
    2. Redistributions in binary form must reproduce the above copyright notice, this list
       of conditions and the following disclaimer in the documentation and/or other materials
       provided with the distribution.
 
 THIS SOFTWARE IS PROVIDED BY Andrea Leofreddi "AS IS" AND ANY EXPRESS OR IMPLIED
 WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND
 FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL Andrea Leofreddi OR
 CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR
 CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR
 SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON
 ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING
 NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF
 ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
 
  * The views and conclusions contained in the software and documentation are those of the
  authors and should not be interpreted as representing official policies, either expressed
  or implied, of Andrea Leofreddi.
```
