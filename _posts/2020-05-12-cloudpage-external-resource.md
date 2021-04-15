---
layout: post
title: "AMPScript Lookup Answers"
categories: [SFMC,AMPScript]
---
Content of a CloudPage is stored on an Akamai CDN thus refreshing a page (cache) may take up to 5 minutes. This little hack saves hundreds of minutes and pulled hairs every month spent on debugging AMPScript or SSJS.  
`%%=TreatAsContent(HTTPGet(“URL”))=%%`