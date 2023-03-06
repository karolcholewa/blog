---
layout: post
title: "Republish Triggered Send Interaction Using SSJS"
categories: [API, SSJS, SFMC]
---

After making changes to a triggered send email you need to republish its interaction. POSTman is a perfect environment for testing triggered send emails, so here is a simple trick to republish interactions directly from POSTman.

## CloudPage with SSJS
Create a CloudPage that executes a script to: pause, publish, and start a selected interaction. The interaction's identifier (that is the CustomerKey), can be queried from a url parameter called for example the *?trigger*.

```javascript
<script runat="server">
    Platform.Load("core", "1");
    var triggername = "";
    triggername = Platform.Request.GetQueryStringParameter("trigger");
    if (triggername == "") {
        Write("{Trigger: underfined, Status: Error}");
    }
    else {
        var tsd = TriggeredSend.Init(triggername);
        var pause = tsd.Pause();
        var publish = tsd.Publish();
        var start = tsd.Start();
        Write("{Trigger:" + triggername + ", Status: updated}");
    }
</script>
```

## Execute the Script from POSTman
POSTman is a great test environment for triggering email. Therefore, it is convinient to republish triggered send interactions directly from the POSTman. Create a GET request using the CloudPage URL and add the interaction's CustomerKey as the *?trigger* parameter value;for example: https://mycloudpagewithssjsscript.com?trigger=CustomerKey


## Resources:

*   [Triggered Send Functions](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/ssjs_triggeredSendFunctions.html)
*   [POSTman GET Request](https://learning.postman.com/docs/sending-requests/requests/)