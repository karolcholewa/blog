---
layout: post
title: "Mobile Studio Notes"
categories: [SFMC]
---

A few practical remarks after spending a few days on troubleshooting the Mobile Studio implementation and using it for **Push** and **SMS** in Journey Builder&hellip;

## Mobile Connect Notes
*   Mobile = multichannel / real-time engagement / location based / convenient
*   Design and applicability is determined by an extra Carrier's dependency
*   Two ways of communication: Mobile Terminated (MT) and Mobile Originated (MO)
*   An SMS Code is an assigned number; a short code is convenient, a long code is a normal, 20-digit number that begins with a country code
*   Short codes are specific to a country, but you can use long codes to reach multiple countries for example Austria and Italy could use the same long code
*   Sender ID is a numeric name, instead of a Long Number; it is one-way only as the Sender ID does not have a number to reply to.
*   FromName can be provisioned or customized, but this feature is not supported in all locales. For example South Africa does not support FromName
*   Keep SMS content within a single message; translated content may be longer and increase cost
*   Create content in Content Builder; access the CB from the main menu (not from the Email Studio)
*   Contact may have more than one Mobile number assigned
*   The **Locale** attribute is important and may cause *Undeliverable*; verify that the Locale is accurate along with the dialing code for example +64xxx-xxx-xxx along with the NZ locale (en_NZ/en-NZ) is correct

## Mobile Push Notes
*   A client's mobile app integrates with SFMC using MobileSDK
*   Device ID pairs with Contact Key after a successful log in to the app process
*   Deleting a Contact from SFMC removes the Device ID pairing, until a new Contact is created and a successful log in to the app is repeated

##  Query Data Views
The **_PushAddress** data view table provides additional demographic data about you Mobile Subscribers. The **_ContactID** is the **SubscriberID** to identify the Contact.


## Resources
*   [Let's Explore Mobile Studio (video)](https://youtu.be/L2oqYb9nmpA?si=zF4HURSSstWkmg2q)
*   [Salesforce MobileConnect – How to Send SMS from Marketing Cloud](https://www.salesforceben.com/the-drip/salesforce-mobileconnect-how-to-send-sms-from-marketing-cloud/)
*   [Keywords and Codes](https://help.salesforce.com/s/articleView?id=sf.mc_moc_managing_keywords_on_short_and_long_codes_in_your_mobileconnect_accounts.htm&type=5)
*   [Interactive Data Views](https://dataviews.io/)