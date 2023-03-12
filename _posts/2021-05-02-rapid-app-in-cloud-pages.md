---
layout: post
title: "Prototype an App in CloudPages"
categories: [AMPscript, HTML, Web]
---

A sample prototype that displays subscriber's data within a CloudPage. It uses CloudPages for hosting, a light-weight HTML/CSS framework, a data extension as a database, and AMPscript to display personalized content.

## E-tickets Distribution and Registration - Case Study
An event organizer sends transactional emails with QR codes to customers who have purchased tickets. The event Staff will scan the e-tickets at the entrance. The Staff would like to quickly respond and solve issues related to e-tickets, such as lost email or discharged or broken mobile phone. Because data for this campaign is already stored in SFMC it can be used and displayed through a CloudPage. A single form to query customer ID and return the ticket holder details and the e-ticket image to scan is enough for a prototype.

## AMPScript Part
This is a simplified AMPScript part to lookup the DE for an entered ID and display e-ticket(s) within the <pre><img></pre> tags.

```javascript
%%[
SET @id = RequestParameter("id") 
SET @rows = LookupRows("QRtickets","ID", @id)
SET @rowCount = RowCount(@rows)
FOR @i = 1 TO @rowCount DO 
SET @row = Row(@rows, 1) 
SET @srcImg1 = Field(@row,"QRCode1")
SET @srcImg2 = Field(@row,"QRCode2")
]%%
```

## HTML
This is an extract of an HTML page that uses the light-weight HTML/CSS framework called **Skeleton**. 

```html
<div class="container">
<div class="row">
<div class="one-half column">
<h2>Show my e-ticket</h2>
<form action="%%=RequestParameter('PAGEURL')=%%" method="post">
<label for="id">Enter Customer ID</label>
<input type="text" name="id">
<input name="submitted" type="hidden" value="true">
<input class="button-primary" type="submit" value="Submit">
</form>
%%[ IF NOT EMPTY(@srcImg1) THEN ]%%
<h5>Your QR Code Ticket 1:</h5>
<img style="width:75%; margin-left:12%" src="%%=V(@srcImg1)=%%">
%%[ ENDIF ]%%
%%[ IF NOT EMPTY(@srcImg2) THEN ]%%
<h5>Your QR Code Ticket 2:</h5>
<img style="width:75%; margin-left:12%;" src="%%=V(@srcImg2)=%%">
%%[ ENDIF ]%%
</div>
%%[ NEXT @i ]%%
</div>
</div>
```
## Adding Skeleton Files to CloudPages
The Skeleton contains only two CSS files (normalize.css and skeleton.css) to control the page grid and the default styling. To add these stylesheets, and any additional CSS, to a CloudPage project, create the **Code Resource** content for each file and refer the URLs in the <head> to the Collection an

## Resources:

*   [Mark Hughes Day 2019 Project Website](/mhday2019)
*   [CloudPages are Public](/cloudpages-are-public)
*   [Zurb Foundation Website](https://get.foundation/)
*   [Skeleton Website (deprecated)](http://getskeleton.com/)
