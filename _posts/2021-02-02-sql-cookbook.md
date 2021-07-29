---
layout: post
title: "SQL CookBook Recipies"
categories: SQL
---

Here is a collection of quick recipies for SQL reports or data digging.

## PATINDEX and LEFT
The PATINDEX function returns a position of a pattern in a string. However, in conjunction with other string functions, such as LEFT it allows you to further extract string patters from a whole. 

For example, a client ID and client email linked by a dash form a subscriberkey like so: 1234567890-client@example.com. To retrieve a client ID from the SubscriberKey do like so:

```sql
SELECT
    LEFT(SubscriberKey, PATINDEX('%-%', SubscriberKey) -1) AS ClientID
FROM
    _Subscribers
```

