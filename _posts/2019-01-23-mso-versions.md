---
layout: post
title: "MSO Versions"
categories: HTML
---


With the plethora of rendering issues that comes with having to support Outlook, it is sometimes useful to target Outlook with specific styles. Fortunately, targeting various versions of Outlook is relatively easy using conditional CSS.

```html
<!--[if gte mso 12]>
    <style>
         ...
    </style>
<![end-if]-->
```

- **lt** is less than a specific version.
- **gt** is greater than a specific version.
- **lte** is less than or equal to a specific version.
- **gte** is greater than or equal to a specific version.
- Outlook 2000 = 9
- Outlook 2002 = 10
- Outlook 2003 = 11
- Outlook 2007 = 12
- Outlook 2010 = 14
- Outlook 2013 = 15
- Outlook 2016 = 16

## Resources
https://litmus.com/community/learning/8-outlook-overview