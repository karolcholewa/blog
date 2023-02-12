---
layout: post
title: "Table Rows with Alternate Color - Part 2"
categories: [AMPscript]
---

This is a second part or another case for using AMPScript to dynamically set a background color to table rows. In this example, I use a process loop to dynamically build a table and then apply a background color to even and odd rows.

## Building a Table Dynamically
Let a sample table display text delivered as delimited string from a 3rd party service (for example SOAP message with XML data). Then the **BuildRowsetFromString** function splits the string and returns a rowset. The number of resulting rows may vary for each message therefore I use the **FOR** statement to iterate through each row from the rowset and build the dynamic, personalized table.

```javascript
%%[
SET @sampleList = "What is Lorem Ipsum? || Where does it come from? || Why do we use it? || Where can I get some?"

SET @rows = BuildRowsetFromString(@sampleList,"||")
SET @rowCount = rowCount(@rows)

IF @rowCount > 0 THEN
]%%

<!--=========Start: Table==========-->
<table>
%%[
  FOR @i = 1 to @rowCount DO
  IF @indicator == "odd" THEN
  SET @color = "#d3d3d3"
  SET @indicator = "even"
  ELSE
  SET @color = "#ffffff"
  SET @indicator = "odd"
  ENDIF
  SET @tableRow = Row(@rows, @i)
  SET @tableCell = Field(@tableRow, 1)
]%%
  <tr><td bgcolor="%%=V(@color)=%%">%%=V(@tableCell)=%%</td></tr>
%%[ NEXT @i ]%%
%%[ ENDIF ]%%
```

## Resources:

*   [AMPscript Guide - BuildRowsetFromString](https://ampscript.guide/buildrowsetfromstring/)
