---
layout: post
title: "Birthday Card Segment"
categories: SFMC
---

Normally, the date of birth attribute should be the **Date** format. This example deals with an exception when date of birth is set as **Text** so it needs to be converted using SQL query. This post is about preparing a segment for a [Birthday Card Email Campaign](/birthday-campaign/). The data extension needs to be sendable (Is Sendable).


## Data Extension Birthday Segment 

For visibility, I included the original date of birth in text (DoB-Text) as the DE column. The other one is converted to Date (DoB-Date) as well as today’s date (it helped me view the data overwrite datestamp).

_Table 1 - Sendable Data Extension for Birthday Segment_

<table>
  <tr>
   <td><strong>Email</strong>
   </td>
   <td><strong>SubscriberKey</strong>
   </td>
   <td><strong>DoB-Text</strong>
   </td>
   <td><strong>DoB-Date</strong>
   </td>
   <td><strong>Today</strong>
   </td>
  </tr>
  <tr>
   <td>email@gmail.com
   </td>
   <td>13579
   </td>
   <td>08/25/1962 00:00:00
   </td>
   <td>Saturday, August 25, 1962 12:00 AM
   </td>
   <td>Saturday, August 25, 2019 7:01 AM
   </td>
  </tr>
  <tr>
   <td>email@yahoo.com
   </td>
   <td>24680
   </td>
   <td>08/25/1983 00:00:00
   </td>
   <td>Saturday, August 25, 1983 12:00 AM
   </td>
   <td>Saturday, August 25, 2019 7:01 AM
   </td>
  </tr>
  <tr>
   <td>email@outlook.com
   </td>
   <td>12345
   </td>
   <td>08/25/1992 00:00:00
   </td>
   <td>Saturday, August 25, 1992 12:00 AM
   </td>
   <td>Saturday, August 25, 2019 7:01 AM
   </td>
  </tr>
</table>



## SQL Query

In my example, I use Date Extension Subscriber Inventory. I has a date of birth (DOB) column but values as in text format. There is no implicit conversion between text and date, in other words comparing value between text and date will return error (or literally stop the Activity with a failure log). I need to convert the text into varchar and then to date. After conversion I can compare today’s date with the date of birth (WHERE).

```sql
SELECT
EmailAddress,
SubscriberKey,
DOB AS DoB-Text,
GETUTCDATE() AS Today,
CONVERT(date, CONVERT(varchar, [DOB])) AS DoB-Date
FROM [Data Extension Subscriber Inventory] mySource
WHERE
MONTH(GETUTCDATE()) = MONTH(CONVERT(date, CONVERT(varchar, [DOB])))
AND
DAY(GETUTCDATE()) = DAY(CONVERT(date, CONVERT(varchar, [DOB])))
```


## Resources

*   [Automation Studio Tutorial](https://youtu.be/A_LabRCwGRc?t=290)
*   [CAST and CONVERT (Transact-SQL)](https://docs.microsoft.com/en-us/sql/t-sql/functions/cast-and-convert-transact-sql?view=sql-server-2017)
*   [Birthday Card Email Campaign](/birthday-campaign/)