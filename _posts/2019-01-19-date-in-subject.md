---
layout: post
title: "Insert Date to the Subject Line"
categories: AMPscript
---


Use this to include a a date or a part of the date in the subject line of an email. For example you want to have an SFMC Report generated for the past 30 days delivered to your inbox and customize the email body or a subject line to include the month that the report.

Here is how:
```javascript
%%[
VAR @prevMonth, @today
SET @today = Now(1)
SET @prevMonth = DateAdd(@today, -1, "M")
]%%

Report for month: %%=Format(@prevMonth, "MMMM, yyyy")=%%
```

## Resources
https://developer.salesforce.com/docs/atlas.en-us.noversion.mc-programmatic-content.meta/mc-programmatic-content/syntaxGuide.htm