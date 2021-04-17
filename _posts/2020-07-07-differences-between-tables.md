---
layout: post
title: "Return Differences Between Two Tables"
categories: SQL
---
You have the two tables Table1 and Table2, both with a Column. To get the records from the Table1 that are **not present** in the Table2 (difference between T1-T2) use the following:


```sql
SELECT T1.Column
FROM Table1 AS T1
    LEFT JOIN
    Table2 AS T2
    ON
    T1.Key = T2.Key
WHERE T2.Column IS NULL
```


To get all the differences with a single query, use the following:

```sql
SELECT
    T1.Column
    ,T2.Column
FROM
    Table1 AS T1
    FULL OUTER JOIN
    Table2 AS T2
    ON
    T1.Key = T2.Key
WHERE
    T1.Column IS NULL
    OR
    T2.Column IS NULL
```


When a record is present in Table1 and not in Table2, the Column from the Table2 is NULL (and the other way around). It is not possible to test for NULL values with comparison operators, such as =, &lt;, or &lt;>. Use the `IS NULL` and `IS NOT NULL` operators instead.


## Alternative Method

```sql
SELECT T1.Column
FROM Table1 AS T1
WHERE NOT EXISTS
    (SELECT T2.Column
    FROM Table2 T2
    WHERE T2.Key = T1.Key)
```

I find the alternate method useful for tables bound using SubscriberKey. For example to find subscribers to whom the email has not been sent. T1 would be a list and the T2 would be the _Sent data view.
