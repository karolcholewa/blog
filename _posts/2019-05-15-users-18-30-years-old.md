---
layout: post
title: "Segment Subscribers Who Are 18-30 Years Old"
categories: SQL
---

This is a useful query for segmenting subscribers 18-30 years old. Normally it's not a big deal if your data is in correct format. The date of birth column I had to use is in text format therefore string functions and casting is necessary. Big Kudos to Jarret from the #emailGeeks Slack channel who helped me with two solutions.

## Simplified solution with manual years entry

```sql
SELECT 
ID, EmailAddress, SubscriberKey, FirstName, LastName, Country
SUBSTRING(myDE.DOB, 1, 10) AS DoB
FROM [My Data Extension] AS myDE
WHERE
SUBSTRING(myDE.DOB, 7, 4) IN ('2001','2000','1999','1998','1997','1996','1995','1994','1993','1992','1991','1990','1989')
```

## Advanced, proper solution with dynamic year calculation

```sql
SELECT 
ID, EmailAddress, SubscriberKey, FirstName, LastName, Country
LEFT([DOB], CHARINDEX('/', [DOB], (CHARINDEX('/', [DOB])+1))+5) AS [DoB]
FROM [My Data Extension]
WHERE YEAR(GETDATE()) - CAST(SUBSTRING([DOB], CHARINDEX('/', [DOB], (CHARINDEX('/', [DOB])+1))+1, 4) AS INT) BETWEEN 18 AND 30
```