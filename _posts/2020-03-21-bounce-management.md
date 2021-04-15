---
layout: post
title: "Bounce Management"
categories: [SFMC,EmailMarketing,SQL]
---

_Bounces are messages that ISPs send back to Marketing Cloud to explain why they can’t deliver your email. When an email can’t be successfully delivered, the application labels the subscriber as Bounced._ To view details about bounced subscribers use the **Bounce** data view. 


## Bounced Recipients for a Job - All Bounces

I’ve sent an email to multiple lists or data extensions and some recipients bounced. I want to pull bounce details for each recipient for a single Job. The query returns a table with all bounced recipients for the _JobID = 1234567890_. The results are as detailed as the date of a bounce, the type, category, or an SMTP message.


```sql
SELECT DISTINCT
    s.[EmailAddress]
    ,s.[SubscriberKey]
    ,s.[Status]
    ,b.[EventDate]
    ,b.[BounceType]
    ,b.[BounceCategory]
    ,b.[BounceCategoryID]
    ,LEFT(b.[SMTPBounceReason],4000) AS BounceReason
    ,b.[SMTPMessage]
FROM
    ENT._Bounce AS b 
INNER JOIN
    ENT._Subscribers AS s
    ON
    b.SubscriberID = s.SubscriberID 
LEFT JOIN 
    ENT._EnterpriseAttribute AS e 
    ON
    b.SubscriberID = e._SubscriberID 
WHERE
    b.[JobID] = 1234567890
```

## Bounced Recipients for a Job - Filtered Bounces

In this surreal example, I want to get details about bounced recipients, but with additional filters. I would like to narrow down the results of bounced recipients only to:


1. Subscribers who are _Students_
2. Subscribers of the _Health and Beauty_ list

This data is available in Subscribers Attributes and to pull it, I need to join the **EnterpriseAttribute** data view.

>   The **LIKE** operator translates to **CONTAINS** for Filters in the click-drag interface. 


```sql
SELECT DISTINCT
    s.[EmailAddress]
    ,s.[SubscriberKey]
    ,s.[Status]
    ,b.[EventDate]
    ,b.[BounceType]
    ,b.[BounceCategory]
    ,b.[BounceCategoryID]
    ,LEFT(b.[SMTPBounceReason],4000) AS BounceReason
    ,b.[SMTPMessage]
FROM
    ENT._Bounce AS b
INNER JOIN
    ENT._Subscribers AS s
    ON
    b.SubscriberID = s.SubscriberID
LEFT JOIN
    ENT._EnterpriseAttribute AS e
    ON
    b.SubscriberID = e._SubscriberID 
WHERE
    b.[JobID] = 1234567890 
    AND
    e.[Subscriptions] LIKE '%Health-and-Beauty%'
    AND
    e.[Occupation]='Student'
```


## Reasons for Held Status

If the system attempts delivery 288 times and the message bounces each time, the subscriber's status is set to Bounced. After Marketing Cloud receives the third bounce for a subscriber, their status is set to Held.

To find out reasons for bounces which eventually led to the Held status, query the _Bounce data view for subscribers whose status is Held. There is no reason to query a specific JobID as Marketing Cloud does not send email to the Held Subscribers.

**Note:** As a result of this query you get each bounce.


```sql
SELECT DISTINCT
    s.[EmailAddress]
    ,s.[SubscriberKey]
    ,s.[Status]
    ,b.[EventDate]
    ,b.[BounceType]
    ,b.[BounceCategory]
    ,b.[BounceCategoryID]
    ,LEFT(b.[SMTPBounceReason],4000) AS BounceReason
    ,b.[SMTPMessage]
FROM
    ENT._Bounce AS b
INNER JOIN
    ENT._Subscribers AS s 
    ON
    b.SubscriberID = s.SubscriberID
LEFT JOIN
    ENT._EnterpriseAttribute AS e
    ON
    b.SubscriberID = e._SubscriberID
WHERE
    e.[Subscriptions] LIKE '%Health-and-Beauty%'
    AND
    e.[Occupation] = 'Student'
    AND
    s.[Status] = 'Held'
```



## Sample Bounce Reasons

To limit the number of characters for the SMTPBounceReason message, I used the LEFT() function with 4000 characters.


<table>
  <tr>
   <td><strong>BounceCategory</strong>
   </td>
   <td><strong>SMTPBounceReason</strong>
   </td>
  </tr>
  <tr>
   <td>Soft bounce
   </td>
   <td>4.2.2 (SMTP reply matched bounce-rcpt pattern rule) The email account that you tried to reach is over quota. Please direct the recipient to <a href="https://support.google.com/mail/answer/6374270?p=OverQuotaTemp">https://support.google.com/mail/answer/6374270?p=OverQuotaTemp</a>
   </td>
  </tr>
  <tr>
   <td>Unknown bounce
   </td>
   <td>Thank you for your e-mail. We will contact you as soon as possible if required.
   </td>
  </tr>
  <tr>
   <td>Soft bounce
   </td>
   <td>5.2.2  Your message to &lt;example@domain.com> was automatically rejected:
<p>
Quota exceeded (mailbox for user is full)
   </td>
  </tr>
  <tr>
   <td>Hard bounce
   </td>
   <td>5.4.1 (no answer from host) Recipient address rejected: Access denied 
   </td>
  </tr>
</table>



## Resources

[Bounce Mail Management](https://sforce.co/2xRvK4W)

[Data Views](https://sforce.co/2QC1QIt)

[SQL Like operator](https://www.w3schools.com/sql/sql_like.asp)

[Common Bounce Codes](https://sforce.co/2J28dki)

