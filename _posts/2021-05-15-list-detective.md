---
layout: post
title: "List Detective (Triggered Sends)"
categories: [SFMC]
---

Some domains, email addresses or even name prefixes may negatively affect deliverability and sender's reputation. SFMC has a tool &ndash; **List Detective (LD)** &ndash; to block inactive domains or known spammers emails. This feature is not enabled by default and to request it log a case with the SF support.

## List Detective for Triggered Sends
The LD automatically checks against an invalid or a known troublesome email addresses. It works while importing subscribers, sending a a data extension, sending a triggered send or collecting data with Web Collect forms.
Despite a custom allowance of specific usernames (whitelisting LD set in the Admin panel for a Business Unit), it won't clear email addresses used in triggered sends. To whitelist LD for triggered sends &ndash; raise a ticket to the SF support.

## Resources:

*   [List Detective documentation](https://help.salesforce.com/s/articleView?id=sf.mc_es_list_detective.htm&type=5))
*   [How to get a list of skipped emails](https://salesforce.stackexchange.com/questions/270126/how-to-get-the-list-detective-data-for-emails-sent-from-a-journey-with-source-as)
*   [REST validateEmail](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/validateEmail.html)
*   [SOAP NotSendEvent Object)](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/notsentevent.html)
*   [Triggered Sends do not honour LD](https://issues.salesforce.com/issue/a028c00000gAx91AAC/triggered-sends-do-not-honour-custom-list-detective-entries)
*   [LD for Triggered Sends Case](https://salesforce.stackexchange.com/questions/198911/list-detective-in-api-trigger-sends-for-transactional)
