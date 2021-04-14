---
layout: post
title: "Viewport and Mobile Pages"
categories: HTML
---
When we compare mobile browsers to desktop ones, the most obvious difference is a screen size. Sites must work on mobile devices, too, so we have to get them to display well on a small screen. The most important problems center on CSS, especially the dimensions of the viewport. If we’d copy the desktop model one-to-one, our CSS would start to misfire horrendously.

A typical mobile-optimized site contains something like the following:

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

This tag, originally Apple-proprietary but meanwhile supported by many more mobile browsers, actually makes the layout viewport fit the device exactly.

Viewport (or the layout viewport) is the area (in CSS pixels) that the browser uses to calculate the dimensions of elements with percentual width, such as div.sidebar {width: 20%}. It’s usually quite a bit larger than the device screen: 980px on the iPhone, 850px on Opera, 800 on Android, etc.
The visual viewport is the part of the page that’s currently shown on the screen.


Without further explanations, if your page does not reflow on a mobile device according to media query rules, step back and check out the doctype declarations and the meta tags.


## Resources

*   https://developer.mozilla.org/pl/docs/Web/CSS/line-height
*   https://medium.com/@zkareemz/golden-ratio-62b3b6d4282a
 

