---
layout: post
title: "Delete Contacts Automatically Using SQL and SSJS"
categories: [SQL, SSJS, SFMC]
---

Deleting Contacts can be a stresful and responsible process. It requires knowledge, prudence, and very often a supervision and approvals of authorities. Here is a shortcut to automated task of deleting unwanted, spare Contacts created from triggered sends.

## Triggered Send Managed List
Triggered emails should either use a publication list (for example All Susbscribers) or a **Triggered Send Data Extension** to manage recipients. Failing to select either one results in storing subscribers related data payload in a hidden, system-defined list called **Triggered Send Managed List**. You should create and select TSDE for each triggered send interaction. However, when an email is sent to a Subscriber who does not exist in All Subscribers, they are appended to All Subscribers after the send. To find such newly appended Subscribers from triggered sends use the following query:

```sql
SELECT EmailAddress, SubscriberKey, [Status]
FROM _Subscribers 
WHERE SubscriberType = 'Unknown External System'
```

## Delete Contacts Using SSJS and Data Extension
In the Contact Builder, you can delete Contacts one by one or select a source of Contact deletion. The same applies to an automated deletion using an SSJS script.
To delete Contacts found and stored to a data extension, use the following script (credit to Elliot Harper).

```javascript
<script language="javascript" runat="server"> 
Platform.Load("core","1.1.5");

// Author: Eliot Harper <eliot@eliot.com.au>
// Revision date: October 24, 2019

// DISCLAIMER
// While due care has been taken in the preparation of this
// supplied code example, no liability is assumed for incidental
// or consequential damages in connection with or arising out its 
// use. Example code is provided on an "as is" basis and no 
// expressed or implied warranty of any kind is made for the 
// suitability of this code for your purpose. Salesforce Marketing 
// Cloud operational procedures and programming methods may change 
// between releases and you are solely responsible for determining 
// whether this code is applicable for your intended use.

var eid = Platform.Function.AuthenticatedEnterpriseID();
var deKey = 'INSERT_DE_KEY';
var clientId = 'INSERT_CLIENT_ID';
var clientSecret = 'INSERT_CLIENT_SECRET';
var authBaseUrl = 'INSERT_AUTH_BASE_URL';

var authUrl = authBaseUrl + 'v2/token/'
var contentType = 'application/json';

payload =  '{';
payload += ' "grant_type": "client_credentials",';
payload += ' "client_id":"' + clientId + '",';
payload += ' "client_secret":"' + clientSecret + '",';
payload += ' "scope": "list_and_subscribers_write",';
payload += ' "account_id": "' + eid + '" ';
payload += '}';

var result = HTTP.Post(authUrl, contentType, payload);
var response = result["Response"][0];
var accessToken = Platform.Function.ParseJSON(response).access_token;
var restUrl = Platform.Function.ParseJSON(response).rest_instance_url;

Platform.Response.Write(" response: " + response);
Platform.Response.Write("\n\n token: " + accessToken);
Platform.Response.Write("\n\n rest URL: " + restUrl);

var headerNames = ["Authorization"];
var headerValues = ["Bearer " + accessToken];

payload =  '{';
payload += '   "deleteOperationType": "ContactAndAttributes",';
payload += '   "targetList": { ';
payload += '      "listType": { ';
payload += '         "listTypeID":3';
payload += '      },';
payload += '   "listKey": "' + deKey + '"';
payload += '   },';
payload += '   "deleteListWhenCompleted":false,';
payload += '   "deleteListContentsWhenCompleted":true';
payload += '}';

var deleteEndpoint = restUrl + 'contacts/v1/contacts/actions/delete?type=listReference';

var result = HTTP.Post(deleteEndpoint, contentType, payload, headerNames, headerValues)

    result = Stringify(result).replace(/[\n\r]/g, '');

Platform.Response.Write("\n\n result: " + result);

</script>
```

## Empty Data Extension Fix
Once you put the SQL Query and the Script activities into an automation if the data extension contains no records to delete, the script activity will throw an error. To prevent from running the script against an empty DE, add the following condition to the **deleteContacts.js**:

```javascript
var deCount = DataExtension.Init(deKey).Rows.Retrieve();

if(deCount.length) {
    var deleteEndpoint = ...
} else {
    Platform.Response.Write("No records to delete");
};
```


## Resources

*   [Find Subscribers from the 'Triggered Send' Managed List](https://help.salesforce.com/s/articleView?id=000387005&type=1)
*   [deleteContacts.js](https://gist.github.com/eliotharper/d1f8c7b4e5b4643e3b9b9da483fa04de)
*   [SFMC Contact Deletion](https://mateuszdabrowski.pl/docs/config/sfmc-contact-deletion/)