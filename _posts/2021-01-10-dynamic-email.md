---
layout: post
title: "Dynamic, Multilingual Email"
categories: AMPScript
---

This post is a case study for building a dynamic email using AMPScript.

Working with multilingual marketing teams in EMEA makes content localization a signIFicant factor in planning digital campaigns (time and money). In this example I streamline a localization process by using data import and AMPScript functions. Not only do I eliminate time spent on building/fixing/testing language versions but also separate content from formatting in the final email.

## Business Requirements
1. It is a transactional email to announce rewards to the winners (no commercial message).
2. A list of recipients (winners) comes from a BI report (Excel file)
3. The email contains personalized content.
4. The text will be translated into 20 languages including RTL (Hebrew/Arabic).
5. IF possible, it should be send as a single email.

### Transactional Email
This is a crucial requirement with less strict CAN-SPAM obligations. It allows a sender to build and send email(s) from a single Business Unit and use a single template without a physical address or an unsubscribe link.

### Sendable and non-sendable data
A sendable data extension has been created from a BI report. It contains mandatory Fields (SubscriberKey) and additional data such as recognitionName, RecognitionLevel achieved, or Language of the recipient.
In addition to the sendable DE, a non-sendable data extension has been created to store translated content.

### Personalization
Starting with a subject line the email has highly personalized content. It uses additional data Fields assigned to each subscriber to form personalized content. Content gradation is based on the RecognitionLevel - higher winners receive more rewards (all should be listed) THEN winners with a lower score.

### Single, localized, dynamic email
A traditional localization of an email content is done by either a translator with access to Content Builder or an email developer who would duplicate an English baseline and create a language-specIFic email copy. It is a resources consuming process as it requires diligence and involvement from each party, proof reading and rendering tests for each email, as well as paying attention to collaborative work and versioning.

A dynamic email approach is very structured. It separates content from appearance. A collaborative work can be done in paralel and in smaller parts that do not require individual tests. An email itself can be built and tested using an English baseline. Marketers/translators who are not comfortable with Content Builder/email development simply fill out an Excel file, column by column and contribute with work at any time of the project.

A single email serves as a template for localized content stored in a non-sendable data extension.


## Email Data

This email campaing uses a BI report with rewards winners (recipients) and content for the email translated into multiple languages.

### Sendable Data Extension - List
Data from a report is manually imported to a sendable data extension. DE text Fields can look like so:
- subscriberKey
- recognitionName
- recognitionLevel
- country
- language

### Non-sendable Data Extension - Content
First, I build an English baseline. THEN I analize content blocks based on a content formatting. Data extension stores clear text amd text formatting is controlled by CSS within the email markup. Each content block is limited to the same formatting rules (font-size, color, font-weight, and so on). THEN I chunk it into content parts like so:
- subjectLine
- content1
- content2
- content3
- disclaimer
- signature
- &hellip;

Content chunks fit into data extension text Fields with tailored lengths. For shorter blocks reserve 50-128 characters and for longer parts 500 characters. Take into account that text size varies in dIFferent languages. 

## Email Content
Text for an email body is stored in rows and columns of a non-sendable data extension. For images I use image content boxes and place them directly in to the email body. Images appearance is toggled using AMPScript. All images are free from text and culturally universal and diversIFied suited for the European culture.

### Inside the Email Body
Content chunks are stored in variables and displayed according to AMPScript rules. The subject line uses text concatenated in a logical, grammatically correct order. 
Formatting can be inline static or dynamic.


![Dynamic Email snapshot](/images/dynamicEmail.png)

## AMPScript Rules

```javascript
%%[
    
    VAR 
        @firstName, @qualificationLevel, @qLevel,
        @colorQL, @language, @subjectLine,
        @content1, @content2, @content3,
        @content4, @content5, @content6,
        @content7, @content8, @disclaimer,
        @signature, @contentBlockID, @rows,
        @rowsEN, @row, @rowCount, @dir

    SET @dir = "" 
    SET @qualificationLevel = Uppercase(AttributeValue("qualificationLevel"))
    SET @language = AttributeValue("Language")
    SET @firstName = ProperCase(AttributeValue("First Name"))
    SET @recognitionName = ProperCase(AttributeValue"recognitionName")) 
    
/*SET the dynamic content based on a language*/
    SET @rows = LookupRows("ContentDE","language",@language) 
    SET @rowCount = RowCount(@rows)

/*Set the English lang as a default*/    
    SET @rowsEN = LookupRows("ContentDE","language","British English") 

/*In case there is no translation, choose English*/
    IF @rowCount > 0 THEN
        SET @row = row(@rows,1)
    ELSE 
        SET @row = row(@rowsEN,1)
    ENDIF
    
    SET @content1 = Field(@row,"content1") 
    SET @content2 = Field(@row,"content2") 
    SET @signature = Field(@row,"signature"
    
/*Depending on a reward, show relevant images and change text color*/
    IF @qualificationLevel == "Bronze" THEN
        SET @contentBlockID = 655024 
        SET @colorQL = "#E08333" 
        SET @qLevel = Uppercase(Field(@row,"bronze"))
    ELSEIF @qualificationLevel == "Silver" THEN
        SET @contentBlockID = 655661 
        SET @colorQL = "#9EACAC" 
        SET @qLevel = Uppercase(Field(@row,"silver")) 
    ELSEIF @qualificationLevel == "Gold" THEN 
        SET @contentBlockID = 655662 
        SET @colorQL = "#FFC605" 
        SET @qLevel = Uppercase(Field(@row,"gold")) 
    ENDIF
    
/*For RTL languages*/ 
    IF @language == "Hebrew" THEN
        SET @dir = "rtl" 
    ENDIF 
]%%
```