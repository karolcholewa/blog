---
layout: post
title: "Migration to Content Builder"
categories: SFMC
---

Content Builder is a lot like a library of content for Marketing Cloud account. These are my notes for consideration when migrating from Classic Email to CB.

Ask a general open question: what problems can you solve with Content Builder?


## Benefits (Why Content Builder)

Apart from a mandatory rollout by Salesforce here are some advantages of CB:


*   Great opportunity to re-organize content; major cleanup
*   Search and Filter; major improvement from literally non-existing in Classic (use naming convention for better filtering and searching capabilities e.g. SKU_description_size_lang; ic_descr_size; event_year_size_lang)
*   Modern approach to creating, organizing and using content (e.g. project-wise approach to organizing folders per campaign – emails, blocks, and images in one place)
*   Improved UI; drag’n’drop tools; repositioning blocks made easy
*   Flexible content Share option (View and Send, Edit Locally, Edit Globally); 
*   Quicker email creation process (e.g. copy and email and use Replace existing content with new content)
*   Import from Classic possible but in fact limited in our context; new templates width is 700px which is incompatible with current 600px wide template and blocks in Classic
*   Test and Preview for individual subscribers
*   Personalization check for up to 5 recipients
*   Code snippets for reusable, more advanced content blocks
*   Improved HTML editor
*   Modern, appealing look&feel
*   Tag content and associate it with campaigns
*   Innovative Content Block SDK that opens new opportunities for custom email widgets (maps, counters)


## Considerations

Content Builder is a lot like a library of content for Marketing Cloud account. 


### Sharing Access



*   Local - everything owned by the current BU
*   Shared - all content that is shared with the current BU or a greater organization
*   You can share individual content or folders.
*   You can share to individual BUs or to all current and future BUs (global org)
*   View and Send - permission for editing; prevents recipients from editing
*   Edit Globally - permission for editing; allows to overwrite original content and will be reflected in all BUs
*   Edit Locally (email only) - allows recipients to make changes within BU; does not overwrite globally


### Importing Content (permission level in Email Studio)



*   The new editor retrieves content only from CB to reduce confusion and searching in Email Studio. It is an opportunity to clean out outdated content.
*   You can import Portfolio, Contents, Templates (also shared)
*   You cannot import Emails/Shared Emails
*   Changes made to content areas in Email Studio/CB does not change the file in one another (unlike images and documents)
*   To better control imported content use Import Content Only
*   Organize content by campaigns, journeys


### Templates



*   You can use existing templates (MR Templates) and use Content Approved legacy content blocks
*   You can create new templates based on the redesigned branding and available content blocks
*   You can add as many blocks to a content area as you want (no one-to-one relationship)
*   Header and Footer should be Locked
*   Paste HTML Templates are more flexible now with additional parameters


### Creating Email



*   Create from template
*   Add Properties
*   Drag and drop content blocks; build and preview simultaneously
*   Use Replace to swap content
*   Preview and Test Send
*   Up to 5 recipients to test an email
*   Code snippets (AMPScript, HTML, etc.)


### Editor



*   Greatly improved (live preview, auto-complete HTML, color coding, line numbers, drag-drop also multiple drag-drop)
*   Drag images directly from computer to email (the image automatically uploads to CB main folder)
*   Scale to Fit for Outlook: keep the image width equal to max template width
*   To paste without the formatting choose Paste as Text Only from the editor toolbar


### Headers and Footers

Library Content in Delivery Profiles does not support Content Builder content. Instead of pulling in header and footer content from Delivery profiles, directly add your header and footer content to an email template in Content Builder. Now that all your content is inside Content Builder, there are several ways to make this work:



*   Build individual header and footer content blocks within Content Builder. Then drag those blocks into your templates and emails or use the Reference block in your emails that reference header or footer blocks.
*   Import existing from Classic content areas into Content Builder using the Import button.
*   Build individual, brand-specific templates with the respective header and footer content. You can create multiple emails using these templates.


### Sending Email



*   Directly from a list of emails
*   Define Properties: subject, preheader
*   Select Audience: find a list
*   Configure Delivery: now or schedule
*   Review details
*   Confirm and Send or Schedule


## Training and Education



*   [https://help.salesforce.com/articleView?id=mc_overview_content_and_email_creation_tools.htm&type=5](https://help.salesforce.com/articleView?id=mc_overview_content_and_email_creation_tools.htm&type=5)
*   [http://salesforce.vidyard.com/watch/Oxi0toiCRGmgh98EGhKsOw](http://salesforce.vidyard.com/watch/Oxi0toiCRGmgh98EGhKsOw)
*   [https://help.marketingcloud.com/get_access_to_content_builder_and_content_canvas/](https://help.marketingcloud.com/get_access_to_content_builder_and_content_canvas/)
*   [https://help.salesforce.com/articleView?id=mc_ceb_get_started_with_content_builder.htm&type=5](https://help.salesforce.com/articleView?id=mc_ceb_get_started_with_content_builder.htm&type=5)
*   [https://help.salesforce.com/articleView?id=mc_ceb_editor_tips.htm&type=5](https://help.salesforce.com/articleView?id=mc_ceb_editor_tips.htm&type=5)
*   [https://help.salesforce.com/articleView?id=Marketing-Cloud-Getting-Started-with-Content-Builder&type=1&language=en_US](https://help.salesforce.com/articleView?id=Marketing-Cloud-Getting-Started-with-Content-Builder&type=1&language=en_US)
*   [https://help.salesforce.com/articleView?id=mc_ceb_content_builder.htm&type=5#mc_ceb_content_builder](https://help.salesforce.com/articleView?id=mc_ceb_content_builder.htm&type=5#mc_ceb_content_builder)
*   [https://help.salesforce.com/articleView?id=mc_overview_content_and_email_creation_tools.htm&type=5](https://help.salesforce.com/articleView?id=mc_overview_content_and_email_creation_tools.htm&type=5)