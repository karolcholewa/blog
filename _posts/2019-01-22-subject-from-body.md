---
layout: post
title: "Create Subject Line Using Body Content"
categories: AMPScript
---


AMPScript is interpreted from top to bottom but the order or operations for email components starts with preheader then HTML body, text body to finally a subject line. This means that you can use content (also dynamic) from an email body and repeat it in a subject line.

In the message body, enter the following line:
```javascript
%%[set @mySubject = "Content from the Body"]%%
```

and then in the subject line field put this part:
```javascript
%%=v(@mySubject)=%%
```