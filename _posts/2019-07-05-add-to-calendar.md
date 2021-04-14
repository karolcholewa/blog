---
layout: post
title: "Add to Calendar"
categories: [EmailMarketing, HTML]
---
There is an open, technical standard called iCalendar that allows applications and systems from many different vendors to transfer calendar information between each other. iCalendar files, which are in fact text files, typically have the file extension ".ICS". ICS files can be imported to or opened in any desktop, web or mobile calendar application such as Apple, Gmail, Outlook, Samsung, Yahoo! and all other.


Google Calendar maintains additional, proprietary standard for calendar meetings and recommends it for a better user experience. Although the .ICS calendar obviously works with the Google Calendar application, users need to download the .ICS file first and then open it with the calendar application. A direct link to a Google Calendar Event triggers the Google Calendar dialog box instantly.


>   TIP: The iCalendar open standard should not be confused with iCal, the former name for the commercial product "Calendar" developed by Apple Computer.


Use this in an invitation email to a webinar or an event. 


## Process:



1. Create an .ICS file using Outlook or the [online tool](https://ical.marudot.com/)
2. Create a Google Calendar Event using the[ online tool](http://kalinka.tardate.com/)
3. Store the ICS (`outlook-event.ics`) on SFMC just like an image; put down the URL to Google Calendar
4. Create Add to Calendar buttons in an email and link to the generated calendars
5. Test the email for your Outlook account and for a Gmail account


## Email Sample 1 (links visible for all recipients)

<div style="color:grey">
Hello Attendees!

Please join our webinar this Friday at 3pm. 
We will present new features for the ACME mobile application.

Add the event to your calendar.

[Apple ](outlook-event.ics) &#124; [Yahoo ](outlook-event.ics) &#124; [Outlook ](outlook-event.ics) &#124; Google 
</div>

## Email Sample 2 (with conditional formatting showing/hiding buttons)

The snippet contains two versions: one is with a button to Google Calendar and ICS visible for all .gmail.com recipient and the second version has ICS calendar only (for non-gmail users that is Apple, Yahoo). More conditions can be created for other Calendars.


```html
<!--CONDITIONAL FORMATTING FOR BUTTONS-->
%%[
var @domain
set @domain = Domain(emailaddr)
]%%
%%[ if @domain == "gmail.com" then ]%%

<!--Google Calendar button-->
<table class="dashedBorder" cellspacing="0" cellpadding="0" border="0" width="100%" style="font-size: 13px;">
	<tbody>
		<tr>
			<td style="background: #ffffff; padding-bottom: 25px; padding-top: 25px;" align="center">
			<table cellspacing="0" cellpadding="0" align="center" border="0">
				<tbody>
					<tr>
						<td style="-webkit-border-radius: 5px; -moz-border-radius: 5px; border-radius: 5px;" bgcolor="#f03a17" align="center"><a href="http://www.google.com/calendar/event?action=TEMPLATE&dates=20181030T120000Z%2F20181030T130000Z&text=Add%20to%20Calendar%20-%20project%20meeting&location=online%20event" target="_blank" style="font-size: 16px; font-family: Helvetica, Arial, sans-serif; font-weight: bold; color: #ffffff; text-decoration: none; -webkit-border-radius: 5px; -moz-border-radius: 5px; border-radius: 5px; padding: 12px 18px; border: 1px solid #f03a17; display: inline-block;">Add To Google Calendar</a></td>
					</tr>
				</tbody>
			</table>
			</td>
		</tr>
	</tbody>
</table>
<!--end of Google Calendar button-->

<!--ICS Calendar button-->
<table class="dashedBorder" cellspacing="0" cellpadding="0" border="0" width="100%" style="font-size: 13px;">
	<tbody>
		<tr>
			<td style="background: #ffffff; padding-bottom: 25px; padding-top: 25px;" align="center">
			<table cellspacing="0" cellpadding="0" align="center" border="0">
				<tbody>
					<tr>
						<td style="-webkit-border-radius: 5px; -moz-border-radius: 5px; border-radius: 5px;" bgcolor="#1186ca" align="center"><a href="outlook-event.ics" target="_blank" style="font-size: 16px; font-family: Helvetica, Arial, sans-serif; font-weight: bold; color: #ffffff; text-decoration: none; -webkit-border-radius: 5px; -moz-border-radius: 5px; border-radius: 5px; padding: 12px 18px; border: 1px solid #1186ca; display: inline-block;">Add To Calendar</a></td>
					</tr>
				</tbody>
			</table>
			</td>
		</tr>
	</tbody>
</table>
<!--end of ICS Calendar button-->
%%[ else ]%%

<!--ICS Calendar button-->
<table class="dashedBorder" cellspacing="0" cellpadding="0" border="0" width="100%" style="font-size: 13px;">
	<tbody>
		<tr>
			<td style="background: #ffffff; padding-bottom: 25px; padding-top: 25px;" align="center">
			<table cellspacing="0" cellpadding="0" align="center" border="0">
				<tbody>
					<tr>
						<td style="-webkit-border-radius: 5px; -moz-border-radius: 5px; border-radius: 5px;" bgcolor="#1186ca" align="center"><a href="outlook-event.ics" target="_blank" style="font-size: 16px; font-family: Helvetica, Arial, sans-serif; font-weight: bold; color: #ffffff; text-decoration: none; -webkit-border-radius: 5px; -moz-border-radius: 5px; border-radius: 5px; padding: 12px 18px; border: 1px solid #1186ca; display: inline-block;">Add To Calendar</a></td>
					</tr>
				</tbody>
			</table>
			</td>
		</tr>
	</tbody>
</table>
<!--end of ICS Calendar button-->
%%[ endif ]%%
```



## Resources

*   [Google Calendar event creator](http://kalinka.tardate.com/)
*   [Add to Calendar from Amit Agarwal](https://www.labnol.org/apps/calendar.html)
*   [ICS calendar appointment creator (Outlook, iCal Apple, other)](https://apps.marudot.com/ical/)
*   [Yahoo Calendar parameters](http://chris.photobooks.com/tests/calendar/Notes.html)
*   [A huge, comprehensive post from Litmus](https://www.litmus.com/blog/how-to-create-an-add-to-calendar-link-for-your-emails/)

