---
layout: post
title: "Template Management"
categories: SFMC
---


This has been published on [LinkedIn](https://www.linkedin.com/pulse/salesforce-marketing-cloud-template-management-karol-cholewa) as well as become a part of the official [Solution Guide in the Salesforce Marketing Cloud](https://sforce.co/3aV4MYM) documentation.


**Single sourcing** and **content reuse strategy** is well known to content manager professionals. Both are my favorite terms in the content management area. Content reuse even appeared to be a _buzzword _over a decade ago. Can content reuse be justified for email marketing templates in Marketing Cloud Content Builder in 2019?

A typical, branded template that I create contains  mobile responsive HTML markup (it is a Paste HTML Template in Content Builder), a header and a footer, and optional elements such as links to social media profiles (Content Blocks). Such template is usually done once and it is used to create hundreds of emails later on. From time to time there are ad-hoc or planned updates to individual or to all templates in the region; for example, links to company resources may change, branding colors were modified, a new email fix has been found by email community, or a major email client posted a release update.

Europe, Middle-East, and Africa may contain over 100 countries and the European Union (EU) itself has 24 official languages. It means that each country requires a separate email template in each officially spoken language. You can distinguish/segment further into commercial and transactional emails and/or customer-based profiles (regular, VIP, prospect, and so on) and things get more interesting. The number of templates for 40 countries and 30 languages may range from 60-200 or more.


# Single-sourced part of the Template

In Marketing Cloud, a single country may be represented as a separate Business Unit. Each unit can use localized templates for local email campaigns.

Branded header and footer are unique parts for each unit (although Austria, Germany, and Switzerland speak more or less the same German language, but some links to company resources vary for each).

The HTML markup is common for every country or a language and** **it is** **a subject to reuse** **across the entire EMEA region. Each country template contains the same HTML layout with CSS styles, media queries, and Outlook conditionals (see _Image 1_).

_Image 1 - Single-sourced HTML Markup reused for multiple email templates_

![Drawing explaining template reuse](/images/SFMC-TemplateManagement.png)


# Same Template, Different Headers and Footers

This is a sample approach for creating emails using single-sourced, shared templates_ _in Content Builder.



1. Start with a template-based email; for the template select the Paste HTML Template.
2. To this new email add a country-specific header and a footer. 
3. You can save this new, blank email as your basic **email template.**
4. To create a new email for a campaign, just duplicate the blank **email template** and content for the campaign. 


Note that the word _Template _in Email Studio is a different content type. The new **email template** is in fact the Template-Based Email that can be duplicated to create a new email. 
The blank **email template **is not necessary but it organizes the email creation workflow (new email starts with “blank canvas”). You can keep this **email template(s) **in a separate folder (Local or Shared) for example the _Templates_ folder. It is especially useful when you have multiple color versions of headers and footers for the same country and users can quickly refer to a specific “email template”. 


### Create an Email Template



1. In the Local folder click **Create **> **Email Message**
2. In the **Define Properties**, select the shared, parent template
3. Click **Next**
4. Name the email the Template-[country]-[language], for example _Template-DE-de_
5. Click **Next**
6. In the **Add Content**, add the** Advanced Content > Reference Content** block and select shared header and the footer
7. Click **Save and Exit**


### Create a New Email Campaign



1. In the Local folder, click **Create **> **Email Message**
2. In the **Define Properties**, **Create Email** section, select **Existing Email**
3. Select the email template for example _Template-DE-de_
4. Add new content, save, and test your email


## Manage the Template Components

_Table 1 - Template Content Sharing and Business Units Permissions_


<table>
  <tr>
   <td><strong>EMEA BU</strong>
   </td>
   <td><strong>Germany BU</strong>
   </td>
   <td><strong>Italy BU</strong>
   </td>
   <td><strong>Spain BU</strong>
   </td>
   <td><strong>UK BU</strong>
   </td>
  </tr>
  <tr>
   <td>HTML Template
   </td>
   <td>x
   </td>
   <td>x
   </td>
   <td>x
   </td>
   <td>x
   </td>
  </tr>
  <tr>
   <td>Header-DE-de
   </td>
   <td>x
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td>Footer-DE-de
   </td>
   <td>x
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td>Header-IT-it
   </td>
   <td>
   </td>
   <td>x
   </td>
   <td>
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td>Footer-IT-it
   </td>
   <td>
   </td>
   <td>x
   </td>
   <td>
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td>Header-ES-es
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>x
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td>Footer-ES-es
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>x
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td>Header-UK-en
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>x
   </td>
  </tr>
  <tr>
   <td>Footer-UK-en
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>x
   </td>
  </tr>
</table>




*   The single Paste HTML Template should be created and kept in the top level, parent Business Unit - for example the EMEA Business Unit. This template **must be** **shared **with all children Business Units (all EMEA countries)
*   Content boxes with localized headers and footers for each country should also be created and kept in the parent EMEA BU (for easier management and to prevent unauthorized users from making changes) but **shared only with specific BU** For example a content box with a German header is shared with Germany only (_View and Send_).
*   In addition, header and footer can be placed in the **email template **as **Reference Content** blocks (instead of simple drag and drop).
*   Any update to the shared HTML Template will be replicated to all template-based emails that use this Template (in all Business Units). Notifications about changes in the HTML Template are visible in the email properties (**Update Email Now**)

_Image 2 - Email Properties Template Changed Notification_


![Update Template Warning in SFMC](/images/SFMC-UpdateTemplate.png)



## Advantages



*   Centralized template management; you can make changes to the shared template/header/footer from a single EMEA BU
*   Access-control; only admin with access to the parent Business Unit can make changes to the shared template/headers/footers.
*   Easy and fast deployment of changes (email hacks, branding styles)
*   Cost efficiency in template creation and maintenance
*   Control email styling using common classes (embedded CSS)


## Disadvantages



*   There is an accessibility issue in using a single template for multiple languages. Each localized template should have a language declaration in the head tag (e.g. lang=”en”). It’s undoable when a single-sourced template serves multiple languages. Language could be declared on a lower, content level though (header, body blocks, footer).
*   For some users, email creation from an Existing Email may not be as intuitive as create email from a Template
*   Users need to pay attention to email Properties and make sure that the template is always up to date (see _Image 2_)


## Resources


### General



*   [EmailGeek - Dynamic Content for Footer](https://youdontneedwp.com/emailgeek/sfmc-dynamic-content-for-footer)
*   [Email On Acid - Email Accessibility](https://www.emailonacid.com/blog/article/email-development/email-accessibilty-in-2017/)
*   [W3.org - HTML Language Declarations](https://www.w3.org/International/questions/qa-html-language-declarations)
*   [https://www.litmus.com/blog/do-email-marketers-and-designers-still-need-to-inline-css/](https://www.litmus.com/blog/do-email-marketers-and-designers-still-need-to-inline-css/) 


### Marketing Cloud



*   [Create Templates](https://help.salesforce.com/articleView?id=mc_ceb_create_templates.htm&type=5)
*   [Add Content to a Template](https://help.salesforce.com/articleView?id=mc_ceb_add_content_to_a_template.htm&type=5)
*   [Add Content to a Paste HTML Template](https://help.salesforce.com/articleView?id=mc_ceb_add_content_paste_html.htm&type=5)
*   [Headers and Footers](https://help.salesforce.com/articleView?id=mc_overview_headers_and_footers.htm&type=5)