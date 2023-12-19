---
layout: post
title: "Transactional Messaging API"
categories: [SFMC, API]
---
A brief exploration of the Transactional Messaging API and a short comparison to Triggered Sends. TM API is a newer version of triggered sends known from the Email Studio. It uses REST API to trigger an event based message and the JSON format to transit data payload for personalization. Sending scenarios are typical to transactional, triggered messages&hellip;

## Integration
Integration between an event triggering/handling service and SFMC requires OAuth2.0 authentication through an Installed Package. Upstream events configuration and triggering calls to specific endpoints varies by implementation and is well documented. Transactional Messaging API supports email, SMS and push messages.

## User Interface
Journey Builder provides a no-code, user interface to create and maintain Send Definitions for triggered emails. Surprisingly, all Journey Builder emails used in regular journeys create Triggered Send Definitions identical to transactional Triggered Sends&hellip;
Transactional journeys are simplified, don't support versioning, don't support other activities.

## Process
The API call executes the Send Definition and the Send Definition sends the email. This is a common, generic scenario for triggering and sending out transactional messages from SFMC. There are a few prerequisites to use TM API:
*   SFMC API user / installed package to authenticate the event triggering service
*   A list of events that trigger the email message
*   A list of unique, External Keys to identify a Send Definition
*   Triggered send data extension to capture Subscribers' attributes needed for dynamic content and personalization

## Send Definition
Each transactional email requires a unique Send Definition. A send defnition contains:
*   Event Definition Key (External Key to identify the transactional api event)
*   Data extension to capture data payload
*   Email Activity
    *   Message Definition (email template)
    *   Message Configuration (Send Classification)
    *   Delivery Options
    *   CC/BCC optional fields

## Triggering a Transactional Message
A sample test message sent using the POST method to: */messaging/v1/email/messages/{messageKey}*

```javascript
{
    "definitionKey": "tm_api_demo_test",
    "recipient": {
        "contactKey": "mySubscriberKey123",
        "to": "myemail@domain.com",
        "attributes": {
            "country": "Italy", 
            "locale": "it-IT",
            "param1": true,
            "param2": 12345,
            "param3": "String1|String2|String3|"
        }
    }
}

```

## Tracking
Messages sent using TM API do not show up in the **Tracking** tool. This is the most noticeable difference compare to Triggered Sends. Tracking is available through the **Intelligence Reports** as well as email get logged to a SendLog.
To overcome tracking limitation the **Event Notification Service** is a preferred choice to monitor anomalies related to mission-critical sends. To implement this additional work is required.

## Summary
*   Transactional Messaging API is a newer solution than its SOAP predecessor
*   It is faster than High Priority Triggered Send and costs one single super message only
*   Triggered Sends are 1-1 compatible with TM API on the following, existing elements:
    *   Dynamic email template + content; reusable across integrations
    *   Email content from data extensions
    *   Triggered send data extensions
*   Transactional Messaging requires a rebuilt of an existing structure (REST endpoints, JSON data format, new Send Definitions)
*   Development work is needed for the event triggering service + the event monitoring/tracking
*   There are some quirks such as: no journey versioning, stopping the journey must be done by Pausing/Resuming otherwise a new event definition is required; Pausing/Resuming works also as republishing content changes

In overall the Transactional Messaging API is a preferred choice for new integrations. It supports email, SMS and Push messages for mission critical transactional communication. However, migrating from legacy Triggered Sends to TM API only for sake of a newer stack may be a controversial and questionable decision.

## Resources
*   [Transactional Messaging API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/transactional-messaging-api.html)
*   [Transactional Messaging - Email](https://developer.salesforce.com/docs/marketing/marketing-cloud/references/mc_rest_transactional_messaging_email/sendMessageSingleRecipient.html)
*   [Transactional Messaging - Errors](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/transactional-send-subscriber.html)
*   [Salesforce Documentation](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/ens.html)
*   [Learn About Transactional Messaging Unit | Salesforce Trailhead](https://trailhead.salesforce.com/content/learn/modules/transactional-messaging/send-transactional-messages)
*   [Monitoring Transactional Emails in Salesforce Marketing Cloud | Salesforce Ben](https://www.salesforceben.com/monitoring-transactional-emails-in-salesforce-marketing-cloud/)
*   [Marketing Cloud — End to End Triggered Email Overview | by Tim Ziter | Cervello, a Kearney Company | Medium](https://medium.com/cervello-a-kearney-company/marketing-cloud-end-to-end-triggered-email-overview-1d8e9a7a0f5c)
*   [A Discussion On Marketing Cloud Triggered Sends | by Charlie Fay | Dec, 2023 | Medium](https://medium.com/@charliefay/a-discussion-on-marketing-cloud-triggered-sends-1b5f9a2c5a2c)
*   [Watch SForce Poland live stream](https://www.youtube.com/live/A20oAWkw9AI?si=sv2lELr8OxKSojTq)
