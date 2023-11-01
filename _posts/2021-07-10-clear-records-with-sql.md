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

#   Clear DE Using SSJS
Sascha Huwald has elaborated on clearing records in [his post](https://www.linkedin.com/pulse/ssjs-clear-entire-data-extension-sascha-huwald/). Here is a method by Gregory Gifford, also from Sascha's post:

```javascript
function clearDE(custKey) {
 var prox = new Script.Util.WSProxy();  
 var action = "ClearData";
 var props = {
     CustomerKey: custKey
 };
 var data = prox.performItem("DataExtension", props, action);
 return data;
}
```

## Resources:

*   [Retrieving and Segmenting Data with a SQL Query Activity](https://help.salesforce.com/s/articleView?id=sf.mc_as_using_the_query_activity.htm&type=5)
*   [SSJS: Clear an entire Data Extension](https://www.linkedin.com/pulse/ssjs-clear-entire-data-extension-sascha-huwald/)