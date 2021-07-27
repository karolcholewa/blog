---
layout: post
title: "Dynamic, Multilingual Email"
categories: AMPScript
---

This post is a case study for building a dynamic email using AMPScript. Data (recipients and content) for the email comes from both sendable and non-sendable data extensions.

Working with multilingual Markets in EMEA makes content localization a significant factor in planning digital campaigns (time and money). In this example I streamline a localization process by using data import and AMPScript functions. Not only do I eliminate time spent on building/fixing/testing language versions but also separate content from formatting in the final email.

## Business Requirements
1. It is a transactional email (rewards announcement with no commercial or marketing content).
2. It is sent to a list created from a BI report.
3. It is a personalized email.
4. Email content will be translated into 20 languages including RTL (Hebrew/Arabic).
5. If possible, it should be a single email Job send

### Transactional Email
This is a crucial requirement as it enables a sender to build and send email(s) from a single Business Unit; for example no physical address is required or a specific link to unsubscribe.
Agreed to use a default, English template for all languages.

### Sendable and non-sendable data
A sendable data extension has been created from a BI report. It contains mandatory fields (SubscriberKey) and additional data such as RecognitionName, RecognitionLevel achieved, or Language of the recipient.
In addition to the sendable DE, a non-sendable data extension has been created to store translated content.

### Personalization
Starting with a subject line the email has highly personalized content. It uses additional data fields assigned to each subscriber to form personalized content. Content gradation is based on the RecognitionLevel - higher winners receive more rewards (all should be listed) then winners with a lower score.

### Single, localized, dynanmic email
A traditional localization of an email content is done by either a translator with access to Content Builder or an email developer who would duplicate an English baseline and create a language-specific email copy. It is a resources consuming process as it requires diligence and involvement from each party, proof reading and rendering tests for each email, as well as paying attention to collaborative work and versioning.

A dynamic email approach is very structured. It separates content from appearance. A collaborative work can be done in paralel and in smaller parts that do not require individual tests. An email itself can be built and tested using an English baseline. Marketers/translators who are not comfortable with Content Builder/email development simply fill out an Excel file, column by column and deliver one's part at any time.

A single email serves as a template for localized content stored in a non-sendable data extension.


## Data

This email campaing uses a BI report with rewards winners (recipients) and content for the email translated into multiple languages.

### Sendable Data Extension - List
Data from a report is manually imported to a sendable data extension. DE text fields can look like so:
- SubscriberKey
- RecognitionName
- RecognitionLevel
- Country
- Language

### Non-sendable Data Extension - Content
First I build an English baseline of the email and analize content blocks with formatting alike. Then I chunk it into content parts like so:
- SubjectLine
- Content1
- Content2
- Content3
- Disclaimer
- Signature
- &hellip;

Content chunks fit into data extension text fields with tailored lengths. For shorter blocks reserve 50-128 characters and for longer parts 500 characters. Take into account that text size varies in different languages. 

## Content
Text for an email body is stored in rows and columns of a non-sendable data extension. For images I use image content boxes and place them directly in to the email body. Images appearance is toggled using AMPScript. All images are free from text and culturally universal and diversified suited for the European culture.

## Email Body
Content chunks are stored in variables and displayed according to AMPScript rules. The subject line uses text concatenated in a logical, grammatically correct order. 
Formatting can be inline static or dynamic.

## AMPScript Rules

```javascript
%%[
    
    var @firstName, @QualificationLevel, @qLevel, @colorQL, @language, @subjectLine, @content1, @content2, @content3, @content4, @content5, @content6, @content7, @content8, @disclaimer, @signature, @contentBlockID, @rows, @rowsEN, @row, @rowCount, @dir

    set @dir = "" 

/*Get values from the sendable DE*/
    set @QualificationLevel = Uppercase(AttributeValue("QualificationLevel"))
    set @language = AttributeValue("Language")
    set @firstName = ProperCase(AttributeValue("First Name")) set @RecognitionName = ProperCase(AttributeValue("RecognitionName")) 
    
/*Set the dynamic content based on Member's language*/
    set @rows = LookupRows("ContentDE","language",@language) set @rowCount = rowcount(@rows)

/*For recipients without translations set English as a default*/    
    set @rowsEN = LookupRows("ContentDE","language","British English") 

/*Check if there is a translation for Member's language*/
    if @rowCount > 0 then set @row = row(@rows,1)
    else set @row = row(@rowsEN,1)
    endif
    
/*Get dynamic content from DE*/
    set @content1 = field(@row,"content1") /*Congratulations*/ set @content2 = field(@row,"content2") /*content2*/       set @signature = field(@row,"signature") 

/*Show the content block with a matching image for each QualificationLevel, set the color for the font, assign localized content*/
    if @QualificationLevel == "Bronze" then
        set @contentBlockID = 655024 
        set @colorQL = "#E08333" 
        set @qLevel = Uppercase(field(@row,"bronze"))
    elseif @QualificationLevel == "Silver" then
        set @contentBlockID = 655661 
        set @colorQL = "#9EACAC" 
        set @qLevel = Uppercase(field(@row,"silver")) 
    elseif @QualificationLevel == "Gold" then 
        set @contentBlockID = 655662 
        set @colorQL = "#FFC605" 
        set @qLevel = Uppercase(field(@row,"gold")) 
    endif
    
/*The rule for Hebrew content; the attribute is placed in each content block on the nearest TD*/ 
    if @language == "Hebrew" then
        set @dir = "rtl" 
    endif 
]%%
```