---
layout: post
title: "SFMC Lookup Answers &ndash; AMPScript"
categories: SFMC
---
These are notes from a Salesforce webinar - *SFMC Lookup Answers* - dedicated to AMPScript.

## TreatAsContentArea

This should actually be renamed to TreatAsContentBlock. It caches a part of the email - common for each subscriber. If you have some statis and dynamic parts, MC won’t render the TreatAsContentArea part but will used the cached resource. This may be an issue for updates as you need to reload the email in JourneyBuilder as changes won’t reflect automatically.

## What the processing order of AMPScript



1. Preheader
2. HTML Body
3. Text Body
4. Subject line

## Tips for testing AMPScript



*   Don’t use SSJS in email - use AMPScript
*   Code for resilience; anticipate every single exception
*   Use RaiseError function in the IF statement

```javascript
%%[
var @debug
var @firstName
set @debug = 1 /*after debugging switch to 0 */
set @firstname = AttributeValue("First Name")
if @debug == 1 then
output(concat("<br>firstName: ", @firstName))
endif
]%%
```
## Can AMPScript use WSProxy

AMPScript has a set of API fuctions which allow to perform SOAP API. It’s not available in email but in script activities and CloudPages. AMPScript API functions can be dropped in favor of WSProxy.

API functions for AMPScript are verbose and follow the API (one-click unsubscribe on springinmoves). The more you understand SOAP objects the broader scope of use.

WSProxy makes it lot easier to use but it is based on SOAP objects - must understand them and their properties. AMPScript API functions are rarely used.

Commonly used SOAP logunsubscribeevent unsubscribe event.

If you use MC Connector and logunsubevent are in sync.

## What’s the difference between Salesforce Data Extension and Marketing Cloud Data Extension:



*   folder location

## Parsing JSON in AMPScript

It does not support JSON now. You can’t parse JSON with AMPScript. You can use GTL which allows you to display JSON on the screen parsed from XML response for instance. You can use AMPScript in combination with GTL.

Adam refuses using GTL in favor of SSJS for parsing.

Pardot uses Mustache and Handlebar personalization language.

## What’s the best practice limit for Lookup



*   Use LookupRows for more than two rows
*   Retrieving from different DEs consider normalizing data to a single DE

## Can you use AMPScript to look information in a sendlog



*   it’s a DE so you could
*   should you?
*   SendLog DE is prone to multiple requests so any additional should be avoided
*   it’s better to copy records to another DE and do operations

## Is it best practice to use AMPScript on CloudPage?



*   AMPScript is good for personalization scripts and HTML - for presentation layer
*   SSJS has error raise and parses JSON
*   You can reference variables between AMPScript and SSJS