---
layout: post
title: "Find a Domain Name in SQL Query"
categories: [SQL]
---
```sql
RIGHT(EmailAddress, LEN(EmailAddress) - CHARINDEX('@', EmailAddress) + 1) as domainName
```

