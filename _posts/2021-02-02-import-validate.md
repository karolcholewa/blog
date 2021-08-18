---
layout: post
title: "Import and Validate Data"
categories: SQL
---

This is about a basic, manual data import from a CVS file to a data extension. Manual file import is prone to a human error which may further result in a poor data quality or mismanagement of a customer consent. That would mean a validation of GDPR.

## Loyalty Program - a Case for Data Import
The NTO company offers a loyalty program for its customers. Every month program participants receive a personalized, summary email. Because the NTO has not integrated their systems yet, data for personalized marketing campaigns arrives in as static Excel files. An email marketer imports data from a file to a data extension and uses personalization strings to deliver specific information to each Subscriber.

## Prepare Data Extensions
This type of a campaign targets existing Subscribers therefore to keep SFMC data reliable and accurate, validate each imported record against the Subscribers database and attributes. You cannot carelessly import customers and emails to a sendable data extension and send a personalized email to each and everyone.

### Non-sendable and Sendable Data Extension
First, plan columns, data types and import data from a report into a non-sendable data extension. This non-sendable data extension does not contain the SubscriberKey nor the EmailAddress columns. Then, use a validation script to join NTO customers from the report with the NTO Subscribers. 
A sample non-sendable data extension (*Raw_NTO_Data*) structure can look like so:

- CustomerID (Text/PrimaryKey)
- Attribute1 (Text)
- Attribute2 (Text)
- Attribute3 (Text)

A sample sendable data extension (*Validated_NTO_Data*) structure can look like so:
- CustomerID (Text)
- Attribute1 (Text)
- Attribute2 (Text)
- Attribute3 (Text)
- SubscriberKey (Text/PrimaryKey)
- Email (EmailAddress)

## Validate Imported Data
After you import raw data from a CSV file to the non-sendable data extension (*Raw_NTO_Data*), you can validate data in a QueryStudio or using a SQL Activity with the resulting, sendable data extension (*Validated_NTO_Data*).

```sql
SELECT
    a.CustomerID
    ,s.SubscriberKey
    ,s.EmailAddress as Email
    ,a.Attribute1
    ,a.Attribute2
    ,a.Attribute3
FROM  [RAW_NTO_Data] a
LEFT JOIN 
    ENT._EnterpriseAttribute e on a.CustomerID = e.[Distributor ID]
INNER JOIN
    ENT._Subscribers s on e._SubscriberID = s.SubscriberID
WHERE s.Status = 'Active'
AND s.[DateUnsubscribed] IS NULL
AND e.[Distributor ID] IS NOT NULL
/*AND e.Subscriptions LIKE '%PL-%'
AND s.Subscriberkey LIKE '%-%' + '%@%'*/
```
This query results in a list of active Subscribers along with additional attributes for personalization.

## Excluded Customers
After validation you may want to send a list of excluded from the email campaign customers to the NTO Customer Support Team so they can reach out to them for example by phone or SMS.

```sql
SELECT
    T1.CustomerID
    ,s.EmailAddress
    ,e.Subscriptions
    ,s.Status
    ,s.[DateUnsubscribed]
FROM [RAW_NTO_Data] AS T1
LEFT JOIN ENT._EnterpriseAttribute e ON T1.CustomerID = E.[Distributor ID]
INNER JOIN ENT._Subscribers s ON e._SubscriberID = s.SubscriberID
WHERE NOT EXISTS
    (
        SELECT T2.CustomerID
        FROM [Validated_NTO_Data] T2
        WHERE T2.CustomerID = T1.CustomerID 
    )
```
