---
layout: post
title: "Lookup Function"
categories: AMPscript
---


This is a very useful AMPScript function that returns a value from data extension. You can specify multiple additional fields and value pairs as part of an AND clause.

## Example 1
Lookup value in a column and return a value from a certain row. The DE is located at: **Data Extensions > MyDataExtension**.
It has multiple columns and it is not a sendable DE - it stores data. 

I want to get an email address for a known value -  I308110304

```javascript
%%[
var @Email, @lookupValue
set @lookupValue = "I308110304"
set @Email = Lookup("MyDataExtension", "Email", "DistributorID", @lookupValue)

]%%

The Member with ID %%=v(@lookupValue)=%% has an email address %%=v(@Email)=%%
```

## Example 2
Lookup multiple columns values from a certain, single row

```javascript
%%[
var @rows, @row, @rowCount
var @lookupValue
set @lookupValue = "I308110304"

set @rows = LookupRows("MyDataExtension","DistributorID", @lookupValue)
set @rowCount = rowcount(@rows)

if @rowCount > 0 then

 var @Email, @FirstName, @LastName
 set @row = row(@rows,1) /* get row #1 */
 set @Email = field(@row,"Email")
 set @FirstName = field(@row,"FirstName")
 set @LastName = field(@row,"LastName")

]%%

%%[ else ]%%

No rows found

%%[ endif ]%%

The Member with ID %%=v(@lookupValue)=%% is name %%=v(@FirstName)=%% and surname %%=v(@LastName)=%% and the email address is %%=v(@Email)=%%
```


## Resources
https://sprignaturemoves.com/ampscript-lookup-examples/