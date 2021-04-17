---
layout: post
title: "Join IDs with Attributes"
categories: SQL
---

A Marketing Team provided IDs of qualifiers who need to be emailed. This is a simple Inner Join in practice to join the IDs with attributes. The ID from the list relates to the ID in the subscribers list.

## SQL Query

If you have an intermediary DE that already contains Subscribers and attributes:

```sql
SELECT
    de.EmailAddress
    ,de.SubscriberKey
    ,de.FirstName
    ,de.LastName
    ,de.ID
FROM
    MyDataExtension AS de
    INNER JOIN
    DataExtensionWithIDs AS id
    ON
    id.ID = de.ID
```

A more generic using Data Views:

```sql
SELECT
    s.EmailAddress
    ,s.SubscriberKey
    ,ea.FirstName
    ,ea.LastName
    ,ea.ID
FROM
    _Subscribers AS s
    LEFT JOIN
    _EnterpriseAttribute AS ea
    ON
    ea._SubscriberID = s.SubscriberID
    INNER JOIN
    DataExtensionsWithIDs AS id
    ON
    id.ID = ea.ID
```