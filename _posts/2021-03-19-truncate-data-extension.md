---
layout: post
title: "Truncate a Data Extension Table"
categories: [SQL, SFMC]
---

To delete millions of records from a data extension you need to go beyond the *Clear records* function on the data extension interface. You want to delete them from a backend.

## Definition
The official Microsoft&reg; documentation for the Transactional SQL language defines the Truncate Table function like so: Removes all rows from a table or specified partitions of a table, without logging the individual row deletions. TRUNCATE TABLE is similar to the DELETE statement with no WHERE clause; however, TRUNCATE TABLE is faster and uses fewer system and transaction log resources.

Sample query

```sql
SELECT *
FROM [MyDataExtension]
```
