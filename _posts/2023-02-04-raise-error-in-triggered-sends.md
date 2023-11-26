---
layout: post
title: "RaiseError() in Triggered Sends"
categories: [SFMC, AMPScript]
---
This post is about using the RaiseError() function with a triggered send. I noticed that after logging an error and skipping the send the number of errors in the triggered send interaction increments too. I asked ChatGPT 3.5 and Microsoft Bing Chat to write this post&hellip;

## The Prompt I Asked
I haven't done any training yet but this is an innevitable learning agenda for 2024. Here is what I asked:

```text
You will write a short blog post about the RaiseError() AMPscript function used to skip a send if a subscriber's custom parameter is equal to a forbidden value. The heading is: "RaiseError() in Triggered Sends" followed by 3-4 paragraphs with a code example:
SET @myParameter = AttributeValue('myParameter')
IF @myParameter== 'Forbidden Value' THEN
    SET @errorMessage = 'This is a forbidden value. Skip the send.'
    InsertDE('RaiseError_LogDE', 'EmailAddress', emailaddr,'EmailName', emailname_, 'ErrorMessage', @errorMessage, 'SubscriberKey', _subscriberkey)  
    RaiseError(@errorMessage, true, 1)
    ENDIF
```

## ChatGPT Answers

### RaiseError() in Triggered Sends

In the world of email marketing, precision and customization are key. Triggered sends allow for tailored, automated messages based on specific subscriber actions or attributes. However, there are times when certain values should prompt the system to halt the sending process. This is where the `RaiseError()` AMPscript function steps in, offering a way to skip a send if a subscriber's custom parameter matches a forbidden value.

The function `RaiseError()` serves a dual purpose: it both logs the issue for future reference and prevents the email from being sent. Let's break down how it works within the context of a triggered send.

Consider a scenario where the custom parameter `@myParameter` is retrieved using `AttributeValue('myParameter')`. If this parameter matches the value `'Forbidden Value'`, it triggers the error handling mechanism:

```ampscript
SET @myParameter = AttributeValue('myParameter')
IF @myParameter == 'Forbidden Value' THEN
    SET @errorMessage = 'This is a forbidden value. Skip the send.'
    InsertDE(
        'RaiseError_LogDE',
        'EmailAddress', emailaddr,
        'EmailName', emailname_,
        'ErrorMessage', @errorMessage,
        'SubscriberKey', _subscriberkey
    )
    RaiseError(@errorMessage, true, 1)
ENDIF
```

In this snippet, the conditional statement checks if `@myParameter` matches the forbidden value. If it does, an error message (`@errorMessage`) is set to indicate the issue. The `InsertDE()` function logs this error into a designated Data Extension (`RaiseError_LogDE`) for future reference. It captures critical details such as the subscriber's email address, the email name, the specific error message, and the subscriber key.

The `RaiseError()` function itself halts the send, preventing the email from being delivered. The first parameter (`@errorMessage`) defines the error message displayed in the system logs or interface. The boolean parameter `true` signifies that this error should be immediately raised. The last parameter, `1`, designates the error's severity level.

By utilizing `RaiseError()` within triggered sends, marketers gain control over the delivery process, ensuring that emails are sent only when the subscriber's attributes align with the desired criteria. This functionality helps maintain data integrity and enhances the overall quality of email communications.

In summary, `RaiseError()` empowers marketers to implement robust error handling within triggered sends, allowing for precise control over email delivery based on specific subscriber attributes. This function acts as a safeguard, preventing sends when critical criteria, like forbidden parameter values, are met, ensuring a more tailored and effective communication strategy.

