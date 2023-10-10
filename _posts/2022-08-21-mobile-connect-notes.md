---
layout: post
title: "Mobile Studio Notes"
categories: [SFMC]
---

This is a work in progress post that collects practical notes from working with the Mobile Studio.

## Mobile Push Notes
*   A client's mobile app integrates with SFMC using MobileSDK
*   Device ID pairs with Contact Key after a successful log in to the app process
*   Deleting a Contact from SFMC removes the Device ID pairing, until a new Contact is created and a successful log in to the app is repeated

## Mobile Connect Notes
*   FromName can be provisioned or customized but this feature is not supported in all locales. For example South Africa does not support FromName
*   Short codes are specific to a country, but you can use long codes to reach multiple countries for example Austria and Italy could use the same long code
*   Keep SMS content within a single message; translated content may be longer and increase cost
*   Create content in Content Builder; access the CB from the main menu (not from the Email Studio)
*   Contact may have more than one Mobile number assigned
*   The **Locale** attribute is important and may cause *Undeliverable*; verify that the Locale is accurate along with the dialing code for example +64xxx-xxx-xxx along with the NZ locale (en_NZ/en-NZ) is correct


## Resources
*   [Salesforce MobileConnect – How to Send SMS from Marketing Cloud](https://www.salesforceben.com/the-drip/salesforce-mobileconnect-how-to-send-sms-from-marketing-cloud/)
*   [Keywords and Codes](https://help.salesforce.com/s/articleView?id=sf.mc_moc_managing_keywords_on_short_and_long_codes_in_your_mobileconnect_accounts.htm&type=5)