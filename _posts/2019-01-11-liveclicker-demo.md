---
layout: post
title: "Liveclicker Demo Evaluation"
categories: [EmailMarketing, Tools]
---

[Liveclicker](https://www.liveclicker.com) is a platform that provides features and enhancements not found in a plain email marketing campaign. You can send to emails with live promos, videos, and **countdowns**. 


## Look and feel/Usability

Although I am quite impressed with the tool itself its usability has some flaws (hidden options e.g. Delete Campaign, too many tabs, horizontal scroll for tabs, no titles or breadcrumbs for the screen, different/duplicated controls to perform the same task) which may be a bit overwhelming at the beginning. Sometimes it reloads or prompts with a warning after each change while setting up a feature – could be annoying.

Nevertheless, it is an easy to use tool that offers advanced configuration panels.

## User Assistance

The tool has rich and accurate documentation, video tutorials, and a support center with articles. Very helpful.

## Demo Test

For each feature, the RealTime Email tool provides only a short HTML snippet to paste into a content box and the rest is just like for any other HTML email. 

## LiveTimer
*   LiveTimer is an animated image - GIF. It is very flexible. In the example it runs over a semi-transparent Extravaganza poster image and after it expires it should show the Extravaganza poster – or any other image that you select. 
*   uses GIF as an image – so pay attention when using a background image for a timer (I used Extravaganza bg to show capabilities of the timer)
*   Updating a countdown timer dynamically updates the content in email - good to prepare a generic counter for campaigns!!!

## LiveImage
*   uses PNG so quality of the input image is preserved. With a bit of creativity this tool can be very impressive to recipients.
*   for MR templates, add MR templates specific classes on IMG tag class="widthFull heightAuto", class="width280 heightAuto", add width, height attributes, add style="display: block"
*   only the large size of an image needs to be loaded to LiveClicker - resize can be done through HTML in the email

## LiveVideo
*   video is a hot topic on the web yet not fully supported in email. The tool offers a wide range of fallback solutions to eventually play back a video on users premises. Worth experimenting in out campaigns
*   full width may present different behavior for our template and become a bit hard to control how it will appear in a final email client (requires thorough tests); not a concern because we are changing to Content Builder
*   I recommend short videos; you need to upload a video file for encoding (animated gif, fallbacks for different email clients).
*   Youtube videos can be encoded directly from YT share links.
*   2-column layout for video is likely to cause formatting issues; use full width instead
*   full control on fallback image and animated GIF timeline (amazing flexibility in one spot)
*   Although the LiveClicker builder is fantastic, using videos in email require thorough tests

## LiveCalendar
*   I used default buttons (Standard/Gmail/Outlook/Yahoo) but the calendar buttons can be customized with any image. Markets will not be able to localize button for already generated LiveCalendar snippet for an event. Instead we could build a generic calendar icon, without text, and each Market could add a call to action to a content box e.g. Add to Calendar/Aggiungi al calendario – that’s an option. Bear in mind that each event requires a new LiveCalendar snippet (different data).

## LiveMap
*   Although I manged to upload a custom location in CSV file, I could not make it work – only the default locations were active in the demo. The LiveMap tool is worth trying as it provides a really usable and cutting edge add-on to email.

## Email Analytics

Not tested

## General impression

I am quite pleased with the RealTime Email features and their use in email marketing campaigns. Each feature considers inconsistencies in email clients (prompts to provide fallback solutions), allows content customization (upload custom images) and personalization using ESP data (%%tag%%).

I did not pay attention to tracking capabilities (impressions) and more advanced features such as targeting rules, A/B testing, deeplinks, geolocation.

 The quality of output images in email is acceptable and, a basic feature setup is straight forward, and the output is as expected.
