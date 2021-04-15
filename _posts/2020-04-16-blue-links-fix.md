---
layout: post
title: "Fixing blue links in Apple and Gmail"
categories: HTML
---


These articles from Litmus explain how to fix auto-linking by Gmail and Apple Mail and iOS devices. Auto-linking results in a default style for all links in email that is blue color and underline.

Add the following markup to a template `<head>` section, within the `<style>` tag:

```css
a[x-apple-data-detectors] {
   color: inherit !important;
   text-decoration: none !important;
   font-size: inherit !important;
   font-family: inherit !important;
   font-weight: inherit !important;
   line-height: inherit !important;
}

.notlink a {color:#78be20!important; text-decoration:none!important;}
```

The **.notlink** class in this example is for branded headings and applies green color to the text. Change it to any other of your branding guidelines.


In the email body, find the headings with address-like section and wrap within the `<span>` tag like so:
```html
<span class="notlink">DOMAIN.COM</span>
```

## Resources

*   [https://litmus.com/blog/how-to-fix-blue-links-in-gmail](https://litmus.com/blog/how-to-fix-blue-links-in-gmail)
*   [https://litmus.com/blog/update-banning-blue-links-on-ios-devices](https://litmus.com/blog/update-banning-blue-links-on-ios-devices)
