---
layout: post
title: "Accessible Emails"
categories: EmailMarketing
---
After over 40 years of existence email became a ubiquitous channel for personal relationship and brands or goods marketing. Similarly to the web, as it has been exposed to a broader audience, email should **overcome limitations** related to disabilities and inabilities of different kinds for human beings. Whether it is impaired hearing, movement, sight or cognitive ability, email and web technology should meet the goal of including everyone with no exceptions.

Here is a brief list of recommended accessibility rules for emails. The subject is broad enough to be a domain on its own but worth mentioning it in my notes. Most inspirations for email accessibility come from Mark Robins - a web and email developer (once RebelMail now Salesforce).

*   Use strong contrast between text and background colours
*   Font size no smaller than 14px for desktop and 16px for mobile
*   Paragraphs aligned to left; 50-60 characters long
*   Line-height: (font-size x 1.5) OR (font-size + 4px)
*   Don’t confuse with animation, too speedy animation or disturbing
*   Use a descriptive subject line
*   Use semantic content &lt;h> and &lt;p> ; add margins for formatting
*   Keep tables to minimum (they are terrible for assistive technology)
*   For every layout table set `role="presentation"`
*   Provide ALT text to images. The screen reader will say "image of..."  then whatever you have in the alt. _“Image of a cat holding a golden gun, riding a fire breathing unicorn over a rainbow”_
*   Use optimized for thumbs bullet-proof buttons for links


## Font-size for mobile


```
@media screen and (max-width: 600px) { p.mobile {font-size: 16px;}}
```



## Fix semantic tags


```
<h1 style="mso-line-height-rule:exactly; Margin:0; font-size:24px; line-height:28px;">This is a title in an email</h1>

<p style="Margin:0; font-size:14px; line-height:18px;">And this is the paragraph</p>
```



## Table presentation role


```
<table role="presentation" aria-hidden="true" cellpadding="0" cellspacing="0" border="0">
<tr>
<td></td>
</tr>
</table>
```



## Resources

*  [Good Email Code by Mark Robins](https://www.goodemailcode.com/)
*   [Mark Robin’s presentation](https://docs.google.com/presentation/d/1GvnKKKIFvjyzly5mvr_LLMKMgD4XNWgj1dlbIpSMkfE/edit?usp=sharing)
*   [https://litmus.com/blog/ultimate-guide-accessible-emails](https://litmus.com/blog/ultimate-guide-accessible-emails)
*   [http://www.emaildesignreview.com/email-industry-insight/accessibility-in-digital-marketing-4148/](http://www.emaildesignreview.com/email-industry-insight/accessibility-in-digital-marketing-4148/)