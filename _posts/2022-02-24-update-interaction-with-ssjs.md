---
layout: post
title: "Update Triggered Send Interactions Using SSJS"
categories: [SSJS]
---

Triggered Sends managed in Email Studio have two components: content and interaction. The latter part provides information about the message and its behaviour each time it's triggered. The Interaction in most cases is created and updated using GUI but in some cases, such as bulk update needed, a short SSJS script saves lots of clicks.

## Add Exclusion Script to Multiple Triggered Send Interactions
This script adds an exclusion script to the triggered send interactions found in the customerKey array.
```javascript
<script runat="server">
  Platform.Load("core","1");
  var customerKeys = ["customerKey_1","customerKey_2","customerKey_3","customerKey_4"];
  var exclusionScript = 'Domain(emailaddr) != "mydomain.com"';
  for (var i = 0; i < customerKeys.length; i++) {
    var customerKey = customerKeys[i];
    var tsd = TriggeredSend.Init(customerKey);
    var pause = tsd.Pause();
    var updateExclusionScript = tsd.Update({"ExclusionFilter" : exclusionScript });
    var start = tsd.Start();
    Write("<p>I paused the interaction " + customerKey + ", updated the exclusion script to " + exclusionScript + " and started the interaction so it's Running</p>");
    }
</script>
```

## Resources
*   [Triggered Sends in Email Studio](https://help.salesforce.com/s/articleView?id=sf.mc_es_triggered_emails.htm&type=5)