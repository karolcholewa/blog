---
layout: post
title: "Try a Different Menu Item"
categories: [SFMC]
---

Back to school starts today and it's a good moment to remind that every problem has usually more than one solution. If a feature stops working in SFMC - check out if it is available from a different menu.

## Script Activity Does Not Validate
I was testing a new script activity using the **Automation Studio**. Apparently, it stopped validating scripts and could not save. Snippets without the `<script>` would validate but yielded no results after execution. Changing a borwser or even requesting SF Premium Support did not sort it out. Multiple 403 errors in the Chrome Dev Console implied changes to security policies.

## Front Door, Back Door, or a Window
Very often large, professional applications allow to accomplish the same task by using different menus, commands or interfaces (GUI or CLI). It may be a result of a requirement to keep the old menu items and duplicate it elsewhere in the new add-on. In my case a script activity did not work from the **Automation Studio** but it worked seamlessly from the **Email Studio > Interaction** menu. Mystery solved or rather worked around.

## Resources
[Email Studio Interactions](https://help.salesforce.com/s/articleView?id=sf.mc_es_interactions.htm&type=5)