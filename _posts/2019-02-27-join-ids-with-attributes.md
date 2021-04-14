---
layout: post
title: "Join IDs with Attributes"
categories: SQL
---

A Marketing Team provided IDs of qualifiers who need to be emailed. This is a simple Inner Join in practice to join the IDs with attributes. The ID from the list relates to the ID in the subscribers list.

## SQL Query

If you have an intermediary DE that already contains Subscribers and attributes:

```sql
SELECT S.[EmailAddress], S.[SubscriberKey], S.[FirstName], S.[LastName], S.[ID]
FROM [myDE] AS S
INNER JOIN [List-IDs] i ON S.[ID] = i.[ID]
```

A more generic using Data Views:
```sql
SELECT S.[EmailAddress], S.[SubscriberKey], A.[FirstName], A.[LastName], A.[ID]
FROM _Subscribers AS S
LEFT JOIN _EnterpriseAttribute AS A ON S.SubscriberID = A._SubscriberID
INNER JOIN [List-IDs] i ON S.[ID] = i.[ID]
```