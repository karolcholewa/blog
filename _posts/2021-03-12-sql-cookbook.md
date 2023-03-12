---
layout: post
title: "SQL Recipies for Data Validation and Reports"
categories: [SQL, SFMC]
---

This is an attempt to create a longer post with a collection of short and sweet recipies for **data validation** and **reports**. The post is intended to grow over time and contain frequently used SQL snippets or scenarios. 

## PatIndex() and Left()
The PatIndex() function returns a position of a pattern in a string. However, in conjunction with other string functions, such as Left() it allows you to further extract string patters from a whole. 

For example, a client ID and client email linked by a dash form a subscriberkey like so: 1234567890-client@example.com. To retrieve a client ID from the SubscriberKey do like so:

```sql
SELECT
    Left(SubscriberKey, PatIndex('%-%', SubscriberKey) -1) AS ClientID
FROM
    _Subscribers
```

## Concat()
To revert the scenario with PatIndex() here is how to combine both ClientID and ClientEmail in order to generate the proper SubscriberKey and exclude any misused SubscriberKeys from a query:

```sql
SELECT
    /*COLUMN*/
FROM
    /*TABLE*/
WHERE
    SubscriberKey = Concat(ClientID, '-', EmailAddress)
```

## CASE
Aliases for link tracking are helpful, but what if you missed a chance to add them before send? This is just another use for the CASE statement. 

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

## Convert()
Profile attributes are stored by the platform as a string type, irrespective of the data types assigned to them. The platform casts them to their assigned type. But what if the assigned type for attributes stored in All Subscribers or a data extension is misused?

For example you want to build a segment for people between age 18 to 40. Date of birth stored in the DOB attribute in a data extension is in text. Here is how to covert it:

```sql
SELECT
    FirstName
    ,LastName
    ,DoB
FROM MyDataExtension
WHERE
    (Year(GetUTCDate()) - Year(Convert(date, Convert(varchar, DoB))) < 41 
    AND
     Year(GetUTCDate()) - Year(Convert(date, Convert(varchar, DoB))) > 17)
```

## Resources
{% for post in site.categories['SQL'] %}
*   [{{ post.title }}]({{ site.baseurl }}{{post.url}})
{% endfor %}