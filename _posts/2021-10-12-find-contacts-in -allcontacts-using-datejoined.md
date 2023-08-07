---
layout: post
title: "Find Contacts From All Contacts Using SQL DateJoined"
categories: [SQL]
---

**All Contacts** in Contact Builder represent all records for all the channels. All Subscribers are Contacts but not the other way around. Therefore you can preview Subscribers or Mobile Contacts separately using Contact Builder or Data Views. Odly enough, there is no unique table to query All Contacts so to find a specific Contact from All Contacts just query the **_Subscribers** table. 

## Filter Contacts Using SQL DateJoined
The **DateJoined** is a very useful column that holds the date the Subscriber joined the All Contacts list. This example helps find Contacts added to a hidden triggered send managed list (antiquated approach to managing triggered send subscribers) in February.

```sql
SELECT SubscriberID
FROM _Subscribers
WHERE SubscriberType = 'Unknown External System'
AND DatePart(Month, DateJoined) = 2
```

## Resources
[How to Delete Subscribers from Hidden Triggered Send Managed Lists in Marketing Cloud](https://help.salesforce.com/s/articleView?id=000381035&type=1)