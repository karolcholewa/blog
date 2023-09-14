---
layout: post
title: "SFDC to SFMC Integration - Best Practices"
categories: [SFMC]
---

Integration between the Salesforce CRM and Salesforce Marketing Cloud is a broad and ambitious subject that deserves attention. It's also a very practical subject that if mastered benefits in out of the box features for data-driven, engaging campaigns. There is already a complete set of documentation for the Marketing Cloud Connect (MCC), integration guides, blog posts. Here are a few quick ones from the **Trailblazer Community** topic.

## A List of Loose Implementation Best Practices For MCC
- Clean up and organize you CRM data
- Plan data import and usage with privacy regulations in mind (GDPR)
- Use the SF ContactID as the ContactKey for SFMC.
- Synchronized Contacts add up to billable records in SFMC
- Set custom boolean fields on the Contact object and sync only relevant Contacts
- To synchronize data between multiple BUs using a single-org Connector, use shared data extensions refreshed with automations
- Use events to trigger Journey Builder entries based on changes in CRM
- Invest in skills
- Maintain internal documentation


## Resources
*   [Looking for Best Practice](https://trailhead.salesforce.com/trailblazer-community/feed/0D54V00007H9p00)
*   [SFMC MCC Integration Patterns](https://mateuszdabrowski.pl/docs/config/sfmc-mcc-integration-patterns/)
*   [MCC Connect Documentation](https://help.salesforce.com/s/articleView?id=sf.mc_co_marketing_cloud_connect.htm&type=5)
*   [9 Key Strategies to Consider While Implementing Salesforce Marketing Cloud](https://www.damcogroup.com/blogs/top-strategies-to-consider-while-implementing-salesforce-marketing-cloud)