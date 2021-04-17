---
layout: post
title: "Compare Lists and Find Same Records"
categories: MSExcel
---

An MS Excel formula to compare two lists with records. Use it to find records from a table A in a table B and highlight or mark with a specific text. It uses `countif` to count cells that meet specific condition. In Marketing Cloud you would use a SQL query to compare two tables but sometimes I need to work on Excel or exported CSV files as well. In this case I add a label "is Active" to the records from the Table A found in the Table B and a label "not Active" to those excluded from the Table B.

## Sample Data


<table>
  <tr>
   <td>Table A     
   </td>
   <td>Table B
   </td>
   <td>Compare
   </td>
  </tr>
  <tr>
   <td>12345     
   </td>
   <td>54321
   </td>
   <td>12345 is Active
   </td>
  </tr>
  <tr>
   <td>678987
   </td>
   <td>12345
   </td>
   <td>678987 not Active
   </td>
  </tr>
  <tr>
   <td>54321
   </td>
   <td>
   </td>
   <td>54321 is Active
   </td>
  </tr>
</table>



## Formula:


```
=IF(COUNTIF($B:$B,$A2),CONCATENATE(A2," is active"),CONCATENATE(A2," not active"))
```


To add a conditional formatting to the text use *Specific Text containing "not active"*, fill with for example red.

To sum up not active users use the following formula:

```
=COUNTIF(C:C,"*not*")
```
