---
layout: post
title: "Baby Shark AMPScript Challenge"
categories: AMPscript
---
This is an AMPScript snippet I submitted for the **Baby Shark AMPScript Challenge** organized by the How-to-SFMC Community. The total number of characters ended up at 361 (no spaces).


```javascript
%%[var @v,@d,@a,@r,@s,@i,@j,@k
set @d=" doo"
set @a="Baby shark*Mommy shark*Daddy shark*Grandma shark*Grandpa shark*Let's go hunt*Run away*Safe at last*It's the end"
set @s=BuildRowsetFromString(@a,"*")
for @i=1 to 9 do
set @r=row(@s,@i)
set @v=field(@r,1)
for @j=1 to 3 do]%%
%%=Concat(v(@v),",")=%%
%%[for @k=1 to 6 do]%%
%%=v(@d)=%% %%[next @k]%%<br>%%[next @j]%%
%%=Concat(v(@v),"!")=%%<br>%%[next @i]%%
```