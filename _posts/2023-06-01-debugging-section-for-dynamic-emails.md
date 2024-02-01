---
layout: post
title: "Debugging Section for Dynamic Emails"
categories: [AMPScript, SFMC]
---
This is a useful block for debugging dynamic email templates. Multiple scenarios require various attribute values and/or additional rule and conditions. A debugging section dynamically displays unique attributes and helps evaluate processed content&hellip;

## Debugging Section - Code Snippet
A debugging section should contain at least a template name and some unique attributes that determine what content displays. The snippet loops through provided, delimited names of attributes (a column name in a sendable data extension) and displays each with a value for a tested Subscriber. 

```javascript
Email name = %%emailname_%%<br>
%%[ 
  SET @rows = BuildRowsetFromString(@attributes, @separator)
  SET @rowCount = RowCount(@rows)
  FOR @i = 1 TO @rowCount DO
  SET @row = Row(@rows, @i)
  SET @attribute = Field(@row, 1)
]%%
  %%=V(@attribute)=%% = %%=AttributeValue(@attribute)=%%<br>
%%[ NEXT @i ]%%
```

## Insert a Debugging Section
To shorten the debugging section, save the snippet in a separate code block and insert the following piece on top of the email template.

```javascript
%%[
  /* List the attributes and variables to debug, and a separator e.g. | */
  SET @attributes = ''
  SET @separator = ''
  

  /* Insert the code snippet with the debugging section */
  Output(ContentBlockById('12345')) ]%%
```
