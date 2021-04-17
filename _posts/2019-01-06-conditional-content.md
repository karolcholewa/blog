---
layout: post
title: "Conditional Content Based on an Email Client"
categories: HTML
---

This is a simple HTML hack for emails. It used to be use to hide an animated GIF for Outlook and show a static image. Currently, the Outlook desktop clients support animated GIFs but the hack is still valid for filtering content based on an email client.

```html
<!--[if mso]>
OUTLOOK CONTENT (STATIC IMAGE)
<![endif]-->

<table style="mso-hide: all">
<tr><td>CONTENT NOT FOR OUTLOOK BUT OTHER CLIENTS</td></tr>
</table>
```



## Resources:

*   [http://freshinbox.com/blog/bulletproof-solution-to-hiding-mobile-content-when-opened-in-non-mobile-email-clients/](http://freshinbox.com/blog/bulletproof-solution-to-hiding-mobile-content-when-opened-in-non-mobile-email-clients/)
*   [https://emailmonks.com/blog/email-coding/show-hide-device-specific-content/](https://emailmonks.com/blog/email-coding/show-hide-device-specific-content/)






