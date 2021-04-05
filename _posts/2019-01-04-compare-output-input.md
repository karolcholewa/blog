---
layout: post
title: "Compare Output List with Input List"
categories: XLSX
---


## Sample Data


<table>
  <tr>
   <td>Input     
   </td>
   <td>Output
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


Add conditional formatting for `Specific Text containing "not active"`, fill with **red**.

To sum up not active users use the following formula: `=COUNTIF(C:C,"*not*")`
