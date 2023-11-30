---
layout: post
title: "API Rate Limiting"
categories: [API, SFMC]
---

In order to keep the system stable and prevent from unexpected or continuous high loads, the SFMC platform limits API requests. As a rule of thumb there is a tolerated limit of 2000 SOAP and 2500 REST calls per minute. Follow best practices, do the math, and you should be fine. Rate limiting does not end at the number of calls though.

## Rate-limiting Reasons
In general rate-limiting happens if you exceed the number of API requests per minute or request an access token too often (20-minute time-to-live). More obscure reasons that force limitations are related to **server utilization** or **database performance degradation**. For example frequent timeouts on SQL queries or retrieving records from a large data extension may result in rate-limiting errors.

## Rate-limiting Consequence
A rate-limited account stops working or works intermittently and unexpectedly. After you remove the rate-limiting root cause the account restores to normal.

## Best Practices
*   Follow SFMC best practices optimizing API calls
*   Control data extension size and sources
*   Monitor automation processes for timeouts and errors
*   Audit access to the platform with an emphasis on API users and integrations
*   Contact Salesforce Support and request a list of anomalies or suspicious process/user behaviors

## Resources:

*   [Best Practices to Prevent Rate-Limiting](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting-best-practices.html)