---
layout: post
title: "Table Rows with Alternate Color - Part 1"
categories: [AMPscript]
---

For a "zebra-striped" effect on table rows (a table to present content not a table to control an email layout), you would use the CSS **:nth-child()** selector. But a quick check with a reference tool [Can I Email](https://www.caniemail.com/features/css-pseudo-class-nth-child/) diminish doubts that any 'fancy' selector is still scarely supported by email clients.


## Static vs Dynamic Table
Static tables come with a known number of rows and columns and are populated with static text for all. Dynamic, personalized tables may contain different amount of information thus a size of a table to display the content is not known. 
For a static table you can apply background colors to all odd and even rows. But for dynamicly built tables you need AMPScript.

## Even-Odd with AMPscript Part 1
I know at least two cases for building a table using AMPScript. Therefore, it is the part one. Let a sample table display values from a data extension columns. Each recipient receives an email that contains a personalized table. A number of rows varies depending on the number of columns with values. Use AMPScript to proactively check whether content is available to create a row and apply a background color. To determine whether it is an even or an odd row, use the modulo operation. 

```javascript
SET @col1row1 = AttributeValue("value1")
```

## Resources:

*   [AMPscript Guide - Mod](https://ampscript.guide/mod/)