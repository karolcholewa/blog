---
layout: post
title: "Find a Domain Name in SQL Query"
categories: [SQL]
---
To add a column with an email domain use the following snippet:
```sql
RIGHT(Email, LEN(Email) - CHARINDEX('@', Email) + 1) AS domainName
```

