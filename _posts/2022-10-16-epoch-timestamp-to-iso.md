---
layout: post
title: "Convert an Epoch/Unix Timestamp to an ISO Format"
categories: [SSJS]
---
An 'epoch' is a the Unix time 0 also a synonym of the 'Unix time'. Unix time format is useless with AMPScript functions. It needs to be converted to a human-format such as ISO 8601. Ideally, you want to receive timestamp attribute values, from upstream systems, in text strings formatted as ISO 8601.Nevertheless, conversion from an Epoch value to ISO value can be done using SSJS&hellip;

## Convert Epoch to ISO for AMPScript
Date&Time functions in AMPScript take arguments in ISO 8601 format, therefore the Unix format should be converted before passing the timestamp values to the AMPScript function. 

```javascript
<script runat="server">
  Platform.Load("core","1");
  var EventTriggeredTimeStamp = Attribute.GetValue("EventTriggeredTimeStamp");
  var timeStamp = new Date(EventTriggeredTimeStamp);
  Variable.SetValue("@timeStamp", timeStamp);
</script>
```

## Format ISO Timestamp Using AMPScript
This is an example of using the FormatDate() function to localize the timestamp in a very elegant way. 

```javascript
SET @locale = AttributeValue("Locale")
SET @timeStampLong = FormatDate(@timeStamp,"l")
SET @timeStampLocalized = FormatDate(@timeStamp,"l","s",@locale)
```
## Resources
*   [ISO 8601 Time and Date Format](https://www.iso.org/iso-8601-date-and-time-format.html)
*   [Unix Time / Epoch](https://en.wikipedia.org/wiki/Epoch_(computing))
*   [Salesforce Stack Exchange](https://salesforce.stackexchange.com/questions/216677/convert-from-epoch-to-datetime-in-ampscript)
*   [Unix Timestamp Converter](https://unixtimestamp.app/)
*   [Epoch Online Converter](https://www.epochconverter.com/)
*   [Unix Timestamp to ISO Converter](https://www.timestamp-converter.com/)
*   [FormatDate() AMPScript Guide](https://ampscript.guide/formatdate/)