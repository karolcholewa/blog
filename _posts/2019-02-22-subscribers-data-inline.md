---
layout: post
title: "Display Subscribers Data Inline With The Name"
categories: AMPScript
---

Marketing Team asked for a bit of dynamic content in a new campaign. Team wanted to know if it was possible to display loyalty points accumulated by a specific Subscriber. The team provided Data Extension with relevant data in columns such as *First_Name, Last_Name, Email, ID, PPV*.

## Email Body

```javascript
%%[
var @firstName, @lastName, @fullName
set @firstName = ProperCase(AttributeValue("First_Name"))
set @lastName = ProperCase(AttributeValue("Last_Name")) /* value from attribute or DE column in send context */
]%%


<p>Hello %%=v(@firstName) v(@lastName)=%%,</p>
<p>Congratulations! You have accumulated %%PPV%% points.</p> 
```

## Subject Line

```
Hello %%=v(@firstName)! You have now %%PPV%% points!=%%
```