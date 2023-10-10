---
layout: post
title: "Regex - Update AMPScript Functions"
categories: [AMPScript]
---
You have set dozens of variables using the **AttributeValue()** function and need to change it to the **Lookup()** function&hellip; This is useful for a very specific case; you want to keep the data source as specified in the Lookup() function and skip any fallback values from Profile Attributes.

##  Data Extensions vs All Subscribers
The All Subscribers list is a default publication list for sendable data extensions. Dynamic, conditional content can use variable evaluation to show/hide content if not empty and so on. All Subscribers Profile Attributes are fallback values for empty values in nullable fields of a sendable data extension. These fallback values may be incorrect or unwanted in some cases. To limit the data source, set variables using the Lookup() function instead of the AttributeValue() function.

##  Regex
To find a replace these strings in an AMPScript email use the following formula.
```javascript
SET @c_dataSource = _DataSourceName

/*Old Format*/
SET @MyAttributeValue = AttributeValue(‘MyAttributeValue’)

/*New Format*/
SET @MyAttributeValue = Lookup(@c_dataSource, ‘MyAttributeValue’, ‘SubscriberKey’, _subscriberkey)
```

### Find the Old Format
```javascript
AttributeValue\('(?<=')(\w.*)'\)
```

### Replace with the New Format
```javascript
Lookup\(@c_dataSource, '$1', 'SubscriberKey', _subscriberKey\)
```

## More Examples

```javascript
SET @c_dataSource = _DataSourceName

/*Old Format*/
SET @myVariable = Lookup(@c_dataSource, 'myVariable', 'SubscriberKey', SubscriberKey)

/*New Format*/
SET @myVariable = Field(@tsdeRow, 'myVariable', 0)
```

### Find the Old Format
```javascript
Lookup\(@c_dataSource, (\'.*?\'), 'SubscriberKey', SubscriberKey\)

```

### Replace with the New Format
```javascript
Field(@tsdeRow, $1, 0)
```

## Resources
*   [RegExr Online Editor](https://regexr.com/)
