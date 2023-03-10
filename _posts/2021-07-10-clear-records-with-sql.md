---
layout: post
title: "Clear Records Using SQL Query Activity"
categories: [SQL]
---

A short 'hack' to clear records from a data extension using a SQL query activity. It's fast and useful in a multistep automation. Use it as a safety measure to clear data from a data extension before loading new data into it in the following step.

```sql
SELECT
NULL AS ColumnName1,
NULL AS ColumnName2,
NULL AS ColumnName3
WHERE 0 = 1
/*Set the Action to Overwrite DE*/
```

## Resources:

*   [Retrieving and Segmenting Data with a SQL Query Activity](https://help.salesforce.com/s/articleView?id=sf.mc_as_using_the_query_activity.htm&type=5)