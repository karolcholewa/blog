---
layout: post
title: "Roles and Permissions"
categories: [SFMC]
---
There are five standard Roles which give access to features related to functions alike. Each role has a set of permissions that allows users perform specific task. It is hard to remember all the combinations but there are three rules for permissions: **explicitly granted, explicitly denied, not explicitly granted/denied**&hellip;

## Standard Roles
The roles are listed from the most to the least access.
*   **MC Administrator** - manages channels, apps, tools, assigns roles to other users
*   **MC Channel Manager** - administers channels, manages omnichannel campaigns
*   **MC Security Administrator** - manages user activity, alerts, and security settings
*   **MC Content Editor/Publisher** - created and sends messages through all the channels
*   **MC Viewer** - can view omnichannel communication activities

## Permissions Matrix
It is hard to remember each Role and its permissions but an **explicitly denied** permission overwrites all other permissions. For the permissions which are **not specifically granted or denied**,  Marketing Cloud **defaults to a deny** permission unless another role grants that permission 

## MC Administrator
All permissions are explicitly granted; all sections available.

## MC Channel Manager
All explicitly granted except the following not explicitly granted (the difference from MC Admin):
*   *General > Role Assignment*
*   *Security > Access*
*   *Security > Manage Watchdog Settings*

## MC Security Administrator
*   *Security > Perform Workgroup Leader Role* - explicitly denied 
*   *Security > Manage Watchdog Settings* - explicitly granted
*   *Access* - explicitly granted in all sections
All other permissions are not explicitly granted or denied.

## MC Content Editor/Publisher
This role has access to most areas but with limited ability to perform actions.
*   *Campaign > Associate* - explicitly granted
*   *Contacts > All Permissions* - explicitly granted
*   *Security > Perform Workgroup Leader Role* - not explicitly granted or denied
All other permissions are explicitly denied.

## MC Viewer
The most restrictive role with only explicitly granted access to general functions, calendar, campaigns and contacts. Every other permission is explicitly denied. 

## Resources
*   [Trailhead Module](https://trailhead.salesforce.com/content/learn/modules/marketing-cloud-roles-and-permissions-quick-look)
*   [Marketing Cloud Roles and Permissions](https://help.salesforce.com/s/articleView?id=sf.mc_overview_roles.htm&type=5)
*   [Marketing Cloud roles & permissions explained](https://horizontal.blog/2020/06/09/marketing-cloud-roles-part-1/)