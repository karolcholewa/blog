---
layout: post
title: "Line-height Fix for CTA in Outlook"
categories: HTML
---

To low line-height set on a cell with content becomes an issue for emails rendered in MS Outlook. Letters with accents (Czech, French, Italian, Polish, Slovak, Slovenian, Portuguese, Romanian, Spanish, Turkish,...) get cut off. Either delete the line-height attribute or set it up high enough to fit in content.

## Issue
An email developer created pre-defined content boxes that contain CTA buttons. The boxes have inline CSS line-height attribute for CTA, paragraphs and headings. Nothing extraordinary if a designer wants to give extra whitespace to paragraphs. Default value depends on the user agent (browser, email client) and in my case the line-height set by the designer inline was equal to value of the font-size...

Although it is a good practice to use relative values, such as % (relative to font-size of the element) I used pixels as Outlook produced unexpected results with percentages. On the other hand using fixed values in pixels may vertically bloat the button on mobile. Therefore I used conditional formatting and fixed the issue for Outlook only.

## Fix
```html
<!-- ALLOWS OUTLOOK DPI SETTINGS TO SCALE TEXT, IMAGES, AND WIDTHS; line-height fix for CTA buttons -->
<!--[if gte mso 9]>
<xml>
        <o:OfficeDocumentSettings>
        <o:AllowPNG/>
   <o:PixelsPerInch>96</o:PixelsPerInch>
        </o:OfficeDocumentSettings>
</xml>
<style type="text/css">
.cta {
  line-height: 24px !important; */the font-size is 16px so it is 150%*/
 }
</style>
<![endif]-->
```

## Resources

*   https://developer.mozilla.org/pl/docs/Web/CSS/line-height
*   https://medium.com/@zkareemz/golden-ratio-62b3b6d4282a
 

