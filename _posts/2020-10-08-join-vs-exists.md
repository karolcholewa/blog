---
layout: post
title: "Join VS Exists"
categories: SQL
---

`EXISTS` is used to return a boolean value, `JOIN` returns a whole other table. `EXISTS` is only used to test if a subquery returns results, and short circuits as soon as it does. `JOIN` is used to extend a result set by combining it with additional fields from another table to which there is a relation.

Use `EXISTS` when:
*   You don't need to return data from the related table
*   You want to check existence (use instead of `LEFT OUTER JOIN...NULL` condition)

`JOIN` syntax is easier to read and clearer normally as well.

## Example

Let’s take the two tables:

1. `Table 1 AS T1` contains only IDs
2. `Table 2 AS T2` could be the EnterpriseAttribute data view.

### Objective
Check if the T1 contains IDs based in Germany (or any other country).


#### Using EXISTS:

```sql
SELECT T1.Key
FROM Table1 AS T1
WHERE EXISTS
    (SELECT Column
    FROM ENT._EnterpriseAttribute AS T2
    WHERE
        T2.Key = T1.Key
        AND
        Country = 'Germany')
```
#### Result

<table>
  <tr>
   <td><strong>T1.Key</strong>
   </td>
  </tr>
  <tr>
   <td>1234567890
   </td>
  </tr>
  <tr>
   <td>0987654321
   </td>
  </tr>
  <tr>
   <td>1324354657
   </td>
  </tr>
</table>

#### Using JOIN: 


```sql
SELECT
    T1.Key
    ,T2.Country
    ,T2.Attribute1
    ,T2.Attribute2
    ,T2.Attribute3
FROM
    Table1 AS T1
    INNER JOIN
    ENT._EnterpriseAttribute AS T2
    ON
    T1.Key = T2.Key
WHERE
    T2.Country = 'Germany'
```

#### Result


<table>
  <tr>
   <td><strong>T1.Key</strong>
   </td>
   <td><strong>T2.Country</strong>
   </td>
   <td><strong>T2.Attribute1</strong>
   </td>
   <td><strong>T2.Attribute2</strong>
   </td>
   <td><strong>T2.Attribute3</strong>
   </td>
  </tr>
  <tr>
   <td>1234567890
   </td>
   <td>Germany
   </td>
   <td><em>value</em>
   </td>
   <td><em>value</em>
   </td>
   <td><em>value</em>
   </td>
  </tr>
  <tr>
   <td>0987654321
   </td>
   <td>Germany
   </td>
   <td><em>value</em>
   </td>
   <td><em>value</em>
   </td>
   <td><em>value</em>
   </td>
  </tr>
  <tr>
   <td>1324354657
   </td>
   <td>Germany
   </td>
   <td><em>value</em>
   </td>
   <td><em>value</em>
   </td>
   <td><em>value</em>
   </td>
  </tr>
</table>



## Resources:


*   [https://stackoverflow.com/questions/7082449/exists-vs-join-and-use-of-exists-clause](https://stackoverflow.com/questions/7082449/exists-vs-join-and-use-of-exists-clause) 
*   [Return Differences Between Two Tables](/differences-between-tables/)