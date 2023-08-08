---
layout: post
title: "Not All Transactional Emails Get Sent"
categories: [SQL]
---

Transactional email classification disregards Subscriber's status. A Subscriber does not need to be Active to receive transactional emails. However, the status **Held** prevents from sending even a transactional message to a held Subscriber.

## Find Held Subscribers and Reactivate
Sometimes it is a single request, and incident reported or a maintenance. Find such Subscriber(s) and update their Status.

```sql
SELECT 
Status,
SubscriberKey,
EmailAddress,
DateJoined,
SubscriberType,
Locale,
BounceCount,
DateUndeliverable
FROM _Subscribers
WHERE Status = 'Held'
```

## Resources
[Change Subscribers Status from 'Held' to 'Active'](https://help.salesforce.com/s/articleView?id=000384663&type=1)