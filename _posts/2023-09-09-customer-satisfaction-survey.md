---
layout: post
title: "Customer Satisfaction (CSAT) Survey"
categories: [AMPScript, SFMC]
---
**Customer Satisfaction (CSAT)** is a metric used by businesses to assess how satisfied their customers are with a specific product, service, or interaction. It provides actionable insights for enhancing customer experiences. This post demonstrates how to prepare Email Studio and CloudPages to send a CSAT survey sent in an email content block.

## Inquiry and Measurements
In a CSAT survey, customers are typically asked a question like: *"How would you rate your overall satisfaction with the service you received?"* The response options are usually graded on a scale, often ranging from 1 to 5, where 1 represents very dissatisfied and 5 represents completely satisfied. It can also be as simple as a **thumb up** or **thumb down**.

The CSAT score is calculated by averaging the responses from customers. This score reflects their level of satisfaction or dissatisfaction with a particular service, interaction, procedure, or product.

## Elements of a CSAT Email Campaign
1. An **CSAT email campaign** or a **CSAT content block** added to a newsletter that contains linked images (the thumb up and the thumb down) to allow Customer's interaction and yield CSAT score (1 or 0).
2. A **Thank You page** built as **CloudPage** to capture Customer's CSAT score and additional attributes from the clicked thumb up/down.
3. A **Data Extension** to store Customer's data, the CSAT score, and additional data for example a response datestamp.

## HTML Email Template
The main purpose of the 'interactive' email is to yield an interaction from Customers and to redirect to a 'thank you page' on which the CSAT score is captured and logged to a data extension.
The email contains the links with the thumb up/down icons:

```html
<body>
    <div class="csat-section">
        <a href="%%=CloudPagesURL(123, 'csatScore', '1')=%%"> <span class="thumbs-up">👍</span></a>
        <a href="%%=CloudPagesURL(123, 'csatScore', '0')=%%"><span class="thumbs-down">👎</span></a>
    </div>
</body>
```
## Thank You CloudPage123
Links in the email redirect to this landing page which has two functions:
1. Captures Customer's data (SubscriberKey, other encrypted attributes) and the CSAT score
2. Shows appreciation to Customers submitting a response to CSAT

### Capture Data and Upsert to CSAT_Data_Extension
A basic version to capture the CSAT score and Customer's data from the email to the data extension using the CloudPage.  It is a good practice to check if a response from the Customer already exists or it is a first time answer.

```javascript
%%[
SET @csatScore = RequestParameter("csatScore")
SET @emailname= RequestParameter("emailname")
SET @subscriberkey =_subscriberkey
SET @email= emailaddr

SET @responseDate = Lookup("CSAT_data_extension", "ResponseDate", "ContactID", @subscriberkey, "EmailName", @emailname)

IF EMPTY(@responseDate) THEN 
    SET @csatData = UpsertData('CSAT_data_extension', 2, 'SubscriberKey', @subscriberkey, 'EmailName', @emailname, 'Rating', @csatScore, 'ResponseDate', Now(), 'ModifiedDate', Now())
ELSEIF NOT EMPTY(@responseDate) AND NOT EMPTY(@csatScore) THEN
    SET @csatData = UpdateData('CSAT_data_extension', 2, 'SubscriberKey', @subscriberkey, 'EmailName', @emailname, 'Rating', @csatScore, 'ModifiedDate', Now())
ENDIF
]%%
```
### Personalized Thank You Page
Having the subscriberkey, additional attributes can be either looked up from another data extension or passed as links parameters. Also the content of the Thank You page can be dynamic based on the feedback.

## Resources
*   [Conversation with Bing]