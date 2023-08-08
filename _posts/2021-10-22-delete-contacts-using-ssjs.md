---
layout: post
title: "Delete Contacts Using SSJS"
categories: [SSJS, SFMC]
---

Contact deletion is an elaborated an sophisticated process. Not due to the number of steps to perform but due to sometimes unforseen repercussions. For example after deleting a Contact you also opt-out that Contact from SMS and Push in the future. **Read twice** the SFMC documentation prior to deleting Contacts especially in larger batches. 

## Sample Process for a Batch Contact Deletion
1. Read twice (documentation), delete once&hellip;
2. Document a request for Contacts delete with explicit, legitimate reasons and required approvals.
3. Find the target Contacts using SQL and load them to a data extension. If Contacts are in a Child BU, use an intermediary shared data extension and import again to a local data extension in the Parent BU.
4. Review random Contacts and make sure you understand consequences for example for Mobile Contacts/Push
5. Use an SSJS script to call the Contact Delete API based on the data extension with targeted Contacts. The script can target a local data extension only (not a shared data extension).

## Resources
*   [Contact Deletion in Contact Builder](https://help.salesforce.com/s/articleView?id=sf.mc_cab_contact_deletion.htm&type=5)
*   [Robert Cameron's SSJS Code to Delect Contacts](https://github.com/camrobert/SalesforceMarketingCloud/blob/main/SSJS%20Contact%20Deletion)
*   [Eliot Harper's Script to Delete Contacts](https://gist.github.com/eliotharper/d1f8c7b4e5b4643e3b9b9da483fa04de)