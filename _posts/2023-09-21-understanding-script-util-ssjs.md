---
layout: post
title: "Understanding Script.Util in SSJS"
categories: [SSJS, SFMC]
---
Think of the `Script.Util` object as a backstage pass holder. It grants access to a set of utility functions to interact with internal and external REST/SOAP APIs. These objects are a part of the **Content Syndication** section of the SSJS documentation.

##  Make HTTP Requests
`Script.Util.HttpRequest`: The all-purpose, powerful tool for making HTTP requests (GET, POST, PUT, DELETE). Use it to interact with external APIs, retrieve data and handle responses. It gives full access to **REST API** calls. To use it with SFMC REST API, it requires an authentication call.

```javascript
<script runat="server">
    Platform.Load("core", "1.1.1")
        
    var accessToken = {{yourToken}};
    var auth = 'Bearer' + accessToken;
    var payload = {
            "firstName": "Carlito",
            "lastName": "EmailGeek",
            "email": "carlitoemailgeek@duck.com"        
            };

    var req = new Script.Util.HttpRequest("https://example.com/users");

    req.emptyContentHandling = 0;
    req.retries = 2;
    req.continueOnError = true;
    req.contentType = "application/json";
    req.setHeader("Authorization", auth);
    req.encoding = "UTF-8";
    req.method = "POST"; //change the method here
    req.postData = Stringify(payload);
    var resp = req.send();

    Platform.Response.Write(resp.content);
</script>
```

##  Just Fetch Data
`Script.Util.HttpGet`: Specifically focuses on making HTTP GET requests. Perfect for when you just want to fetch data from an external resource. To execute it use the `Script.Util.HttpGet.send()` method; it returns the **HttpResponse** object.

```javascript
<script runat="server">
    Platform.Load("core", "1.1.1")

    var req = new Script.Util.HttpGet("http://www.example.com/users");
    var resp = req.send();

    Write(resp.content);
</script>
```

## Returned HTTP Responses
`Script.Util.HttpResponse`: a returned object from the send() method. This is a CLR format object and must converted to a string before parsing it further to the JSON format.

```javascript
<script runat="server">
Platform.Load("core", "1.1.1")
try {
    var req = new Script.Util.HttpGet("http://www.example.com/users");
    var resp = req.send();

    if (resp.statusCode == 200) {
        var content = resp.content();
        var respContent = content.Platform.Function.ParseJSON(String(content));
        for(var i=0; i<respContent.length; i++) {
            Write("<p>First Name: " + respContent[i].firstName + "</p>");
            Write("<p>Last Name: " + respContent[i].lastName + "</p>");
            Write("<p>Email: " + respContent[i].email + "</p>");
        }
    }
    else {
        Write("Errors found<br>");
        Write("Error code: " + resp.statusCode(); + "<br>") 
    }
}
catch(e) {
    Write(Stringify(e));
}
</script>
```

## WSProxy
`Script.Util.WSProxy`: A kind of the VIP pass to accomplish **SOAP API** calls. Use WSProxy to retrieve data, create records, and update objects from nearly any SOAP API that needs to interact with SFMC. To make a call, it uses native authentication of the user performing the call, meaning that there is no need to provide any auth calls.


## Resources
*   Conversation with Bing
*   [Salesforce documentation on SSJS](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/ssjs_serverSideJavaScript.html)
*   [Script.Util.HttpRequest](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/ssjs_platformContentSyndicationScriptUtilHttpRequest.html)
*   [Script.Util.HttpGet](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/ssjs_platformContentSyndicationScriptUtilHttpGet.html)
*   [Script.Util.HttpResponse](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/ssjs_platformContentSyndicationScriptUtilHttpResponse.html)