---
layout: post
title: "Birthday Card Email Campaign"
categories: HTML
---

Marketing Cloud used to have **Playbooks** to create common campaigns such as on-boarding, anniversary, or birthday emails. I never used Playbooks which eventually have been retired and replaced by Journey Builder templates.

To create a simple Birthday campaign I used **Automation Studio** as follows:

1. Create a Birthday Segment and a SQL Query Activity to import data daily
2. Create a Birthday Email and a Send Email Activity to send an email daily
3. Create an Automation and schedule it to run daily


## SQL Query Activity

A date of birth needs to be imported as an attribute in All Subscribers or a column in Data Extension. You can compare the day and the month from the birthday date to today’s date values. Assuming that both are represented by the same data type (Date) it is relatively easy. Make sure this Date Extension **Is Sendable** - you will send the Birthday emails to this list.

I covered a scenario with some data conversions [in this post.](https://youdontneedwp.com/emailgeek/sql-birthday-segment)


## Send Email Activity

Create a nice, personalized Birthday email, test, and use it for for the Send Email Activity. 


## Automation

Create a scheduled automation to run daily in the morning (for example at 7 am). In the first step you run SQL query to overwrite data in the Birthday segment and in step two send the Birthday email. 


## Resources

*   [Automation Studio tutorial](https://youtu.be/A_LabRCwGRc?t=290)
*   [Send Email Activity Help Page](https://help.salesforce.com/articleView?id=mc_as_send_email_activity.htm&type=5)
*   [https://youdontneedwp.com/emailgeek/sql-birthday-segment](https://youdontneedwp.com/emailgeek/sql-birthday-segment)

