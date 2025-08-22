---
layout: post
title: "Return Differences Between Two Tables"
categories: SQL
---
You have the two tables Table1 and Table2, both with a Column. To get the records from the Table1 that are **not present** in the Table2 (difference between T1-T2) use the following:


```sql
SELECT ColumnName
FROM Table1
WHERE ColumnName NOT IN (
    SELECT ColumnName FROM Table2
)
```
