---
layout: post
title: "Conditional content based on an email client"
categories: [HTML, EmailHack]
---

This is a simple HTML hack for emails. It was useful for example to hide an animated GIF for Outlook and show a static image instead. Nowadays, Outlook desktop clients support animated GIFs but the hack is still valid for hiding content depending on an email client.

```HTML
<!--[if mso]>
OUTLOOK CONTENT (STATIC IMAGE)
<![endif]-->

<table style="mso-hide:all">
<tr><td>CONTENT NOT FOR OUTLOOK BUT OTHER CLIENTS (ANIMATION)</td></tr>
</table>
```



## Resources:



*   [http://freshinbox.com/blog/bulletproof-solution-to-hiding-mobile-content-when-opened-in-non-mobile-email-clients/](http://freshinbox.com/blog/bulletproof-solution-to-hiding-mobile-content-when-opened-in-non-mobile-email-clients/)
*   [https://emailmonks.com/blog/email-coding/show-hide-device-specific-content/](https://emailmonks.com/blog/email-coding/show-hide-device-specific-content/)






