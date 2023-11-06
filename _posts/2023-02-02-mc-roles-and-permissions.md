---
layout: post
title: "Marketing Cloud Roles and Permissions"
categories: [SFMC]
---
There are five standard Roles which give access to features related to functions alike. Each role has a set of permissions that allows users perform specific task. In addition to the MC Roles, there are four Email Studio or Classic Roles. While it is hard to remember all the combinations, there are three rules for the permissions: **explicitly granted, explicitly denied, not explicitly granted/denied**&hellip;

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

## Email Studio aka Classic Roles
It is probably due to the ExactTarget legacy but in addition to the MC Roles there are four additional Email Studio roles:
*   **Administrator** - all permissions, related to Email Studio, explicitly granted 
*   **Analyst** - full access to the Tracking area
*   **Content Creator** - general access plus full access to Content and Shared Classic Content
*   **Data Manager** - full access to everything in Email Studio except email content

By default all MC roles have the following expansion permissions to Email Studio: *Access System Default Email Templates*, *General Access*. In addition there are a few other additional permissions for each MC role for the Email Studio, therefore the Classic Roles expand MC Roles within the Email Studio.

## The Real SFMC Admin
Assign both the **MC Administrator** and the **Administrator** roles to a full fledged, power Admin.

## Resources
*   [Trailhead Module](https://trailhead.salesforce.com/content/learn/modules/marketing-cloud-roles-and-permissions-quick-look)
*   [Marketing Cloud Roles and Permissions](https://help.salesforce.com/s/articleView?id=sf.mc_overview_roles.htm&type=5)
*   [Marketing Cloud roles & permissions explained](https://horizontal.blog/2020/06/09/marketing-cloud-roles-part-1/)