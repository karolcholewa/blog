---
layout: post
title: "Accessible CTA Button"
categories: [HTML]
---
This is a summary/extract from **Paul's Airy** article about the Web Content Accessibility Guidelines (WCAG) and importance of the target size for call to action (CTA) **buttons and links**. While browsers render the ```<button>``` or the `<input>` tags properly making the entire bounding box clickable, in email it requires a bit more scrutiny&hellip;

## Accessible Buttons
According to the **Success Criterion 2.5.5 Target Size (Enhanced)**, a selectable area of a target should be 44px X 44px minimum. Therefore, the entire area of a CTA button should be selectable, not just its text. As buttons are constructed with anchor tags to meet the requirems apply padding around the `<a>` tag as follows:

```html
<a href="" target="_blank" 
style="font-family:Arial, sans-serif; font-size:18px; 
line-height:1.1em; font-weight:bold; color:#ffffff; 
text-decoration:none; text-align:center; 
padding:0.75em 1em; display:block;">Call to Action</a>
```

## Accessible Links
The new feature of the **Success Criterion 2.5.5 Target Size (Enhanced)** helps solving a problem when two or more links are placed to close to each other and thus become harder targets. A remedy to this is a 24px X 24px bounding box around the links.

## Conclusion Quoted From Paul Airy
*   While Success Criterion 2.5.8 Target Size (Minimum) introduces a target size of 24px x 24px, I recommend conforming to Success Criterion 2.5.5 Target Size (Enhanced), with a target size of 44px x 44px, on buttons, to ensure they’re fully selectable.
*   Conform to Success Criterion 2.5.8 Target Size (Minimum) on smaller elements such as text links and social media icons.
*   Consider the location of links when writing copy.
*   Check that your text links bounding boxes don’t intersect one another.
*   Familiarise yourself with WCAG 2.2.


## Resources
*   [Paul Airy Blog](https://beyondtheenvelope.cmail19.com/t/d-e-vtlody-jlaiyail-a/)
*   [WCAG Success Criterion 2.5.5 Target Size (Enhanced)](https://www.w3.org/TR/WCAG22/#target-size-enhanced)
*   [WCAG Success Criterion 2.5.8 Target Size (Minimum)](https://www.w3.org/TR/WCAG22/#target-size-minimum)
*   [WCAG Bounding Box Definition](https://www.w3.org/TR/WCAG22/#dfn-bounding-boxes)
*   [Accessible Emails](/accessible-emails/)