---
layout: post
title: "Dynamic Bullet List with AMPScript"
categories: [AMPscript]
---

A snippet to build a bullet list using a process loop in AMPscript. It simply demonstates how to replace repetitve lines of AMPscript with a shorter process loop. There are at least two more practial cases to use a dynamic bullet list for example a bullet list from a delimited string.

```javascript
//======BEFORE=======
%%[
SET @c_bulletPoint1 = Field(@content,"Bullet1",0)
SET @c_bulletPoint2 = Field(@content,"Bullet2",0)
SET @c_bulletPoint3 = Field(@content,"Bullet3",0)
SET @c_bulletPoint4 = Field(@content,"Bullet4",0)
SET @c_bulletPoint5 = Field(@content,"Bullet5",0)
]%%
<ul>
    %%[IF NOT Empty(@c_bulletPoint1) THEN]%%
    <li>%%=V(@c_bulletPoint1)=%%</li>
    %%[ENDIF]%%
    %%[IF NOT Empty(@c_bulletPoint1) THEN]%%
    <li>%%=V(@c_bulletPoint2)=%%</li>
    %%[ENDIF]%%
    %%[IF NOT Empty(@c_bulletPoint1) THEN]%%
    <li>%%=V(@c_bulletPoint3)=%%</li>
    %%[ENDIF]%%
    %%[IF NOT Empty(@c_bulletPoint1) THEN]%%
    <li>%%=V(@c_bulletPoint4)=%%</li>
    %%[ENDIF]%%
    %%[IF NOT Empty(@c_bulletPoint1) THEN]%%
    <li>%%=V(@c_bulletPoint5)=%%</li>
    %%[ENDIF]%%
</ul>   

//======AFTER=======
<ul>
%%[ VAR @counter
    FOR @counter = 1 TO 5 DO
    SET @c_bulletPoint = Field(@content,Concat('Bullet',@counter),0)
]%%
    %%[IF NOT Empty(@c_bulletPoint) THEN]%%
    <li style="padding-bottom:15px">%%=V(@c_bulletPoint)=%%</li>
    %%[ENDIF]%%
%%[ NEXT @counter ENDIF]%%
</ul>   
```