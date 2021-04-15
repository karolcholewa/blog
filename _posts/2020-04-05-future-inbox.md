---
layout: post
title: "The Future of the Inbox - Webinar Notes"
categories: EmailMarketing
---


These are notes from the Salesforce webinar “The Future of the Inbox”.


## Actions in Email

Good for enhancing design, content and layout.



*   Gallery (good for showing multiple images of a product)
*   Tabs (titles and content blocks below)
*   Accordion (title expands to reveal a section)
*   Hotspots (fashion brands)

**Support:** Gmail, Outlook webmail, Yahoo!, AOL


## Forms Submit in Email

Complete a form and submit from inside the email. Data will be passed to a landing page.



*   Profile
*   Reviews (generate twice as many reviews
*   Survey (
*   B2B Lead forms

**Support:** Gmail, Yahoo, AOL, webmail 


### Fallback

For users who won’t see the interactive version:



*   Always think about a fallback
*   Sometimes the fallback can be no fallback
*   **Forms**: link to an online version of the form
*   **Accordions & tabs**: show expanded content or link to the full content on the website
*   **Gallery**: choose a main image or 2
*   One subject line needs to cover every version of the email


## AMP for Email



*   Can make emails interactive
*   You can keep content up to date
*   Take actions right from inside (survey etc)
*   Compatible with existing email

**Support (additional MIME type): **Gmail, Mail.ru, Outlook developer, Yahoo coming soon.


## Designing For Interactive



*   Interactive HTML email and AMP work very well alongside each other, whether you are using one the other or both you always need to consider your fallback content
*   You only have one subject line, that needs to cover all versions of the email
*   Use recognisable design conventions to make it easier for the user to understand they can interact
*   **Don’t be afraid to call it out too, instruct your users how they can interact**
*   The motivation for adding these **enhancement **should always be user experience, don’t do it to be cool and flashy, do it to improve **the experience** 


## Designing For AMP



1. **Purpose**. Do dynamic elements support the emai’s intended purpose?
2. **Discovery**. Are users aware of interactive elements?
3. **Navigation**. Does the nav structure of the email complement its purpose?
4. **Confirmation**. Are actions supported in the email followed by feedback on status, success, or failure? (undo)
5. **Short & sweet**. Are dynamic elements scoped to the scale of an email? Does it link out when appropriate?
6. **Accessibility**. Is the email accounting for accessibility best practices?


## Dark Mode for Email

Dark Mode is taking over the inbox - and making sure emails look great in this reading environment is the new big challenge for email marketers.


### Why dark mode?



*   It can be easier on the eyes
*   Reduced screen brightness can save battery life
*   It can improve legibility for some users
*   People prefer it aesthetically


### Three levels of support in email clients: 



1. No color changes; regardless color settings
2. Partial color invert
3. Full color invert


### How to Enable Dark Mode


```
@media (prefers-color-scheme: dark)

/* Outlook.com and Outlook Android app supports data attributes */

[data-ogsc] and/or [data-ogsb]
```



### What should you update?



*   Image backgrounds and contrast
*   Background colors
*   Text colors and contrast
*   Call-to-action


## Build Privacy and Trust

Understand and respect your subscribers. If you respect privacy and send right emails subscribers start to trust you.


### Privacy Laws

Privacy laws around the world are constantly changing:


### Personally Identifiable Information (PII) or Personal Data



*   Employee Data
*   Subscribers (email addresses)
*   Through Products
*   Defined as Data Controllers and Data Processors


### Laws and Regulations



*   CASL - Canada
*   PIPEDA - Canada
*   US Federal and State Laws
*   CCPA (California)
*   Brazil
*   GDPR - EU and UK


### DMARC

We cannot trust you, consumer cannot trust you, without DMARC. Authenticated emails provide trust. At some point no emails without DMARC will be allowed.


### BIMI

Brand Indicators for Message Identification is an industry-wide standards effort that will use **brand** logos as **indicators** to help people avoid fraudulent email, while giving marketers a huge new opportunity to put their **brands** in front of consumers for free.

96% of emails come from brands - no faces; logo builds trust in your inbox.


## Use Structured Data

Structured data is additional information along with the core CSS and HTML send with an email campaign. 



*   Enhances the subscriber experience
*   Provides important information at a glance
*   Largely relies on established standards

Gmail annotations are powered by structured data.

Yahoo! mail extracts information using both Schema.org and other methods.

Structured data allows to go beyond email mailbox experience. You can deliver information when needed NOT when receive it - in other words, content within context. For example a coupon displayed at the store or a trip itinerary during a trip.


## Voice Assistants and Email

You can imagine future when voice assistant look into structured data or more advanced usage.


### Voice-Enabled Devices



*   Google Assistant
*   Microsoft Cortana
*   Amazon Alexa
*   Apple Siri


### Capabilities



*   Read through inbox
*   Read emails
*   Archive
*   Reply 
*   Delete


## Assistive Technology


### Screen Readers



*   NVDA
*   JAWS
*   VoiceOver
*   Narrator
*   ChromeVox


### Voice Input



*   Dragon
*   Apple Voice Control
*   Windows Dictation


### What To Do



*   Code semantically
*   Don’t break established conventions
*   Avoid image-only emails
*   Write simply, use clear calls-to-actions


## Reader View

It looks in the code, strips out the styles and adjusts to users preferences. Reader views allows users to pull content and present in the most digestible way.

Semantic coding is required.

**Support**: Outlook.com, browsers (e.g.Chrome extension)


##  Resources

[https://emailclientmarketshare.com/](https://emailclientmarketshare.com/) 

[https://go.amp.dev/learn-email](https://go.amp.dev/learn-email)

[https://amp.gmail.dev/playground/](https://amp.gmail.dev/playground/)

[https://g.co/dev/ampemail](https://g.co/dev/ampemail) 

[https://bimigroup.org](https://bimigroup.org) 

[https://schema.org](https://schema.org) 

[https://litmus.com/blog/the-ultimate-guide-to-dark-mode-for-email-marketers](https://litmus.com/blog/the-ultimate-guide-to-dark-mode-for-email-marketers)

[https://www.salesforce.com/products/marketing-cloud/resources/webinars/](https://www.salesforce.com/products/marketing-cloud/resources/webinars/)
