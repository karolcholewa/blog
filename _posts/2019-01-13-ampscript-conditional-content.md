---
layout: post
title: "Conditional Content Based on Subscriber Attributes"
categories: AMPScript
---


The Dutch team asked to find a way and deliver English content to Dutch subscribers residing in Malta, while Dutch users would still receive content in their native language.

Consider two simple options: 
1. Exclusion list 
2. Conditional content

Here is a snippet that handles dual content and serves it based on Subscriber Attribute - in this case this is a country of residency:

```javascript
%%[
var @CoR
set @CoR = AttributeValue("Residence Country")
]%%

%%[ if @CoR == "MT" then ]%%
<p>This is a para in English for MT users</p>
%%[ else ]%%
<p>Dit is een paragraaf in het Nederlands.</p>
%%[ endif ]%% 
```

## Resources

[https://developer.salesforce.com/docs/atlas.en-us.noversion.mc-programmatic-content.meta/mc-programmatic-content/attributevalue.htm?search_text=AttributeValue](https://developer.salesforce.com/docs/atlas.en-us.noversion.mc-programmatic-content.meta/mc-programmatic-content/attributevalue.htm?search_text=AttributeValue)

[https://ampscript.guide/book/attributevalue/](https://ampscript.guide/book/attributevalue/)
