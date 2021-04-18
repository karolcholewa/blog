---
layout: post
title: "Counting, Grouping, and Sorting"
categories: SQL
---


A few tips on grouping, counting or simply showing unique values.


## Show a Unique List of Records

If there is a Table1 with users from different countries, represented in the columns UserID and Country, to list a distinct list of countries (the country will occur once only)  - use `DISTINCT`.

```sql
SELECT DISTINCT
    UserID
    Country
FROM
    Table1
```

### Result
A list of countries or country codes, which you can use as a filter criteria.


## Count UserIDs for Each Country

If there is a Table1 with users from different countries, represented in the columns UserID and Country, to list the countries and show the number of UserIDs for each country, use the aggregate function `COUNT()` and the `GROUP BY` statement.

### from github
{% gist 7088b85691e0402d996e7721801c11e64354e9c3 %}

```sql
SELECT
    COUNT(UserID)
    ,Country
FROM
    Table1
GROUP BY
    Country
```

### Result
A list of countries or country codes with a corresponding number of users for each.

## Count and Sort Users for Each Country

If there is a Table1 with users from different countries, represented in the columns UserID and Country, to list the countries and show the number of UserIDs for each and then sort them, use the aggregate function `COUNT()`, the `GROUP BY` and the `ORDER BY` statement with the `TOP` clause.


```sql
SELECT TOP 500
    COUNT(UserID)
    ,Country
FROM
    Table1
GROUP BY
    Country 
ORDER BY
    COUNT(UserID)
DESC
```

