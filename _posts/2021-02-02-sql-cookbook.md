---
layout: post
title: "SQL CookBook Recipies"
categories: SQL
---

This is a collection of quick recipies for SQL reports or data digging. This post is incremental not to create short posts for quick SQL queries and tips.

## PATINDEX and LEFT
The PATINDEX function returns a position of a pattern in a string. However, in conjunction with other string functions, such as LEFT it allows you to further extract string patters from a whole. 

For example, a client ID and client email linked by a dash form a subscriberkey like so: 1234567890-client@example.com. To retrieve a client ID from the SubscriberKey do like so:

```sql
SELECT
    LEFT(SubscriberKey, PATINDEX('%-%', SubscriberKey) -1) AS ClientID
FROM
    _Subscribers
```

## CONCAT
To revert the scenario with PATINDEX here is how to combine both ClientID and ClientEmail in order to generate the proper SubscriberKey and exclude any misused SubscriberKeys from a query:

```sql
SELECT
    /*COLUMN*/
FROM
    /*TABLE*/
WHERE
    SubscriberKey = CONCAT(ClientID, '-', EmailAddress)
```

## CASE
Aliases for link tracking are helpful, but what if you missed a chance to add them before send?

Just another use for the CASE statement. 

```sql
SELECT
    CASE
        WHEN LinkName LIKE 'https://domain.com/articles/%' THEN 'Link to an article'
        WHEN LinkName LIKE 'https://shop.domain.com/%' THEN 'Link to e-commerce'
    END AS LinkAlias
FROM _Click
WHERE JobID = '12345'
```

## Did Not Open for X Days
To find subscribers who opened an email up to five days ago:

```sql
SELECT DISTINCT s.SubscriberKey
FROM _Sent s
LEFT JOIN _Open o ON s.SubscriberKey = o.SubscriberKey
WHERE DateDiff(day, s.EventDate, GetUTCDate()) <= 5
AND o.SubscriberKey is NULL
```

To find subscribers who did not open an email for the past 90 days:

```sql
SELECT s.SubscriberKey
FROM _Subscribers s
WHERE s.SubscriberKey NOT IN
        (SELECT o.SubscriberKey
        FROM _Open o
        WHERE o.EventDate >= DateAdd(day, -90, GetDate())     
        )
```