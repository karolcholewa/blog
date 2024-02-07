---
layout: post
title: "Debugging Section for Dynamic Emails"
categories: [AMPScript, SFMC]
---
This is a useful block for debugging dynamic email templates. Multiple scenarios require various attribute values and/or additional rules and conditions. A debugging section shows you the attributes you're using and how they affect the dynamic content&hellip;

## Debugging Section - Code Snippet
In a debugging section, it's essential to include a template name and specific attributes that dictate the displayed content. The code snippet iterates through the delimited attribute names (which correspond to column names in a sendable data extension) and presents each one along with its associated value for a tested Subscriber or a scenario.

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
  /* Enter attributes to debug and a separator for example the '|' */
  SET @attributes = ''
  SET @separator = ''
  
  /* Insert the code snippet */
  Output(ContentBlockById('12345')) ]%%
```
