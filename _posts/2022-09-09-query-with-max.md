---
layout: post
title: "Query a Sendlog for Latest Emails"
categories: [SQL]
---
A short and very useful query to find X latest emails logged in a sendlog. This can be any DE really to query&hellip;

```sql
SELECT TOP 10 MAX(SendTime), view_email_url
FROM SendLog
WHERE emailname = 'my_email_template' AND Locale = 'it-IT'
GROUP BY view_email_url
ORDER BY Max(SendTime) DESC
```

