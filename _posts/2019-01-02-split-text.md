---
layout: post
title: "Split Text String at a Specific Character"
categories: MSExcel
---

An MS Excel formula especially useful to split a full name into first and last name.

## Example 1
Given a string separated by space: **Jimmy James**

To get the left part of the string, us the following formula:

```
=LEFT(B2,FIND(" ",B2)-1
```

To get the right part of the string, us the following formula:

```
=RIGHT(B2,LEN(B2)-FIND(" ",B2))
```


## Example 2
Given a string separated by comma: **Johny , Ryall**

To get the left part of the string, us the following formula:

```
=LEFT(B3,FIND(" , ",B3)-1)
```

To get the right part of the string, us the following formula:

```
=RIGHT(B3,LEN(B3)-FIND(",",B3)-1)
```






