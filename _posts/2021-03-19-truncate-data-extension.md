---
layout: post
title: "Truncate a Data Extension Table"
categories: [SQL, SFMC]
---

To delete millions of records from a data extension you need to go beyond the **Clear records** function on the SFMC graphical user interface. You want to delete them from a backend&hellip;

## T-SQL Truncate Table Statement
The official Microsoft&reg; documentation for the Transactional SQL language defines the Truncate Table statement like so:
> Removes all rows from a table or specified partitions of a table, without logging the
> individual row deletions. TRUNCATE TABLE is similar to the DELETE statement with no
> WHERE clause; however, TRUNCATE TABLE is faster and uses fewer system and transaction
> log resources.

SQL Query activities in SFMC support only the SELECT statement that is for reading a neither for inserting, updating nor deleting records in a data extension. Therefore, to delete a mass amount of records using SQL use a workaround.

## Workaround
Create a basic SQL Query activity, select a source *MyDummyDE* that contains a single, dummy record and overwrite the target, bulky data extension with that single record.

```sql
SELECT *
FROM [MyDummyDE]
```
