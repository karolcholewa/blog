---
layout: post
title: "Convert an EPOCH Timestamp to ISO Format"
categories: [SSJS]
---
An 'epoch' is a the Unix time 0 also a synonym of the 'Unix time'. Unix time format is useless with AMPScript functions. It needs to be converted to a human-format such as ISO. Ideally, you want to receive ISO values of the timestamp attribute, but conversion from an Epoch value to the ISO value can be done using SSJS&hellip;

## Convert Epoch to ISO

```javascript
<!--Converting Unix time to a valid format for AMPScript--> 
<script runat="server">
  Platform.Load("core","1");
  var EventTriggeredTimeStamp = Attribute.GetValue("EventTriggeredTimeStamp");
  var timeStamp = new Date(EventTriggeredTimeStamp);
  Variable.SetValue("@timeStamp", timeStamp);
</script>
```

## Format ISO Timestamp Using AMPScript

```javascript
SET @timeStampLong = FormatDate(@timeStamp,"l")
SET @timeStampLocalized = FormatDate(@timeStamp,"l","s",Locale)
```
## Resources
*   [Salesforce Stack Exchange](https://salesforce.stackexchange.com/questions/216677/convert-from-epoch-to-datetime-in-ampscript)
*   [Epoch Online Converter](https://www.epochconverter.com/)
*   [FormatDate() AMPScript Guide](https://ampscript.guide/formatdate/)