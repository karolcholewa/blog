---
layout: post
title: "Convert an Epoch/Unix Timestamp to an ISO Format"
categories: [SSJS, AMPScript]
---
An 'epoch' is a the Unix time 0 also a synonym of the 'Unix time'. Unix time format is useless with AMPScript functions. It needs to be converted to a human-format such as ISO 8601. To convert a timestamp to a date format, simply use the SSJS to create a new Date object&hellip;

## Convert Epoch to ISO for AMPScript
Date&Time functions in AMPScript take arguments in ISO 8601 format, therefore to pass a datestamp to the FormatDate() AMPScript function, create a Date object for the original timestamp.

```javascript
<script runat="server">
  Platform.Load("core","1");
  var originalTimeStamp = Attribute.GetValue("originalTimeStamp");
  var myTimeStamp = new Date(originalTimaStamp);
  Variable.SetValue("@timeStamp", myTimeStamp);
</script>
```

## Format ISO Timestamp Using AMPScript
This is an example of using the FormatDate() function to localize the timestamp in a very elegant way. 

```javascript
SET @locale = AttributeValue("Locale")
SET @timeStampLong = FormatDate(@timeStamp,"l")
SET @timeStampLocalized = FormatDate(@timeStamp,"l","s",@locale)
```
## A Trouble with a Time Offset in AMPScript
The ISO timestamp format provides an offset value related to the UTC (Z as the Zulu time means zero offset). If the offset is "+02:00," it means that the local time is 2 hours ahead of UTC.
If the offset is "-05:30," it means that the local time is 5 hours and 30 minutes behind UTC. The offset is an essential part of the ISO 8601 format because it allows you to specify the exact time zone in which a date and time are expressed, making it easy to convert and compare times across different time zones accurately.
Passing a timestamp with an offset to the **FormatDate()** function returns the time in UTC! Trying to calculate the offset using the **getTimeZoneOffset()** JavaScript function complicates the things further, as the local time is the SFMC server time that is UTC-6. Interetingly enought a web version of an email (view in browser link) may vary further if a browser local settings are used for calculations&hellip;
To format and show the local time I simply trimmed the offset part.

## Resources
*   [ISO 8601 Time and Date Format](https://www.iso.org/iso-8601-date-and-time-format.html)
*   [Unix Time / Epoch](https://en.wikipedia.org/wiki/Epoch_(computing))
*   [Salesforce Stack Exchange](https://salesforce.stackexchange.com/questions/216677/convert-from-epoch-to-datetime-in-ampscript)
*   [Unix Timestamp Converter](https://unix timestamp.app/)
*   [Epoch Online Converter](https://www.epochconverter.com/)
*   [Unix Timestamp to ISO Converter](https://www.timestamp-converter.com/)
*   [FormatDate() AMPScript Guide](https://ampscript.guide/formatdate/)