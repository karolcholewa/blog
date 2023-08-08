---
layout: post
title: "Find One of Each Kind of the Records"
categories: [SQL]
---

A short SQL snippet to find single records of different kind. For example one of each Clients that speak different languages.

## Sample Process for a Batch Contact Deletion
```sql
SELECT Min(SubscriberKey) as SubscriberKey, Language
FROM [myDataExtension]
GROUP BY Language
```