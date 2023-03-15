---
layout: post
title: "Pull More with Data Views"
categories: SQL
---

Data Views store tracking information related to Contacts and the system, for example automations performance. They are a useful tool for troubleshooting whether a message has been sent out to a subscriber. Here is a simple scenario when and how to use data views in conjunction with custom reports from business.

## Scenario
A Sales department sent in a report with customerID, SubscriberKey, email addresses and countries of residence of people who should be emailed about XYZ campaign. The data has been uploaded to a sendable DE and filtered into DE for each country. A campaign has been sent out.

The next day after sending the campaign I was asked to deliver a **list of names** of people who were emailed. This data wasn’t a part of a report but it is kept in Marketing Cloud profile attributes.

## Solution

You can run these and similar queries without creating resulting DEs by using the **Query Studio** application. The tool creates temporary, lasting for 24 hours, non-sendable DEs. The resulting DEs are available in the *QueryStudioResults* folder. You can rename the DEs and export to CSV report files.
I split this simple task, for sake of clarity, into the following smaller parts:

1. Filter the master DE into each country and match the records with SubscriberKeys using the **Subscribers** data view
2. Pull names using the **EnterpriseAttribute** and **Sent** data views
3. Optional: Check who’s already opened the email using the **Open** data view
4. Combine all intermediary DEs into the final DE that will be a final report for the Business Team


## Match the report with Subscribers in SFMC
Usually the SubscriberKey will not be a part of a report but for sake of clarity it is in this example. To match the records from the imported DE with those which are subscribers in SFMC, join the DE with the Subscribers data view:

```sql
SELECT
    de.CustomerID
    ,de.Email
    ,de.Country
    ,s.SubscriberKey
FROM
    MyReport AS de
    INNER JOIN
    ENT._Subscribers AS s
    ON
    s.SubscriberKey = de.SubscriberKey
WHERE
    Country = 'UK'
```

Name the resulting DE as *UkSubscribers*.

## Pull First Name and Last Name (*UkSubscribersNames*)
Once you have a DE in SFMC and need to pull more attributes, such as FirstName, LastName join the table with the EnterpriseAttribute data view. Because not everyone from the sendable DE was a recipient (status counts) join the list with the Sent data view for more precision.

```sql
SELECT
    de.CustomerID
    ,ea.FirstName
    ,ea.LastName
    ,de.Email
    ,de.Country
    ,de.SubscriberKey
FROM
    UkSubscribers AS de
    LEFT JOIN
    ENT._EnterpriseAttribute AS ea
    ON
    ea.CustomerID = de.CustomerID
    INNER JOIN
    ENT._Sent AS s
    ON
    de.SubscriberKey = s.SubscriberKey
```

Name the resulting DE as *UkSubscribersNames*

## Check Who Has Already Opened the Email
You can add extra information to the report such as - who's already opened the email sent (JobID) using the Open data view:

```sql
SELECT
    de.CustomerID
    ,de.FirstName
    ,de.LastName
    ,de.Email
    ,de.Country
    ,o.EventDate AS [OpenDate]
    ,de.SubscriberKey
FROM
    UkSubscribersNames AS de
    INNER JOIN
    ENT._Open AS o
    ON
    de.SubscriberKey = o.SubscriberKey
WHERE
    o.JobID = 123456789
    AND
    uo.IsUnique = 1
```

Name the resulting DE as *UkSubscribersOpens*


## Final Report
You can combine all the generated DEs into a single one like so:

```sql
SELECT
    CustomerID
    ,Email
    ,FirstName
    ,LastName
    ,Country
    ,OpenDate
FROM
    UkSubscribersNames AS de
    FULL OUTER JOIN
    UkSubscribersOpens AS o /*null will appear if not opened*/
    ON
    de.SubscriberKey = o.SubscriberKey
```


## Resources:



*   [https://sfmarketing.cloud/2019/08/22/data-views-in-salesforce-marketing-cloud/](https://sfmarketing.cloud/2019/08/22/data-views-in-salesforce-marketing-cloud/)
*   [https://help.salesforce.com/articleView?id=mc_as_sql_reference.htm&type=5](https://help.salesforce.com/articleView?id=mc_as_sql_reference.htm&type=5)
*   [https://help.salesforce.com/articleView?id=mc_as_data_view_open.htm&type=5](https://help.salesforce.com/articleView?id=mc_as_data_view_open.htm&type=5)
*   [https://svgshare.com/i/Edm.svg](https://svgshare.com/i/Edm.svg)