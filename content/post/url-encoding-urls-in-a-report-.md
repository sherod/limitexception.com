+++
author = "Steven Herod"
date = 2014-03-28T00:00:00Z
description = ""
draft = false
slug = "url-encoding-urls-in-a-report-"
title = "URL encoding URLs in a Report."

+++


Recently I had a slightly interesting requirement.

A [URL field](http://www.salesforce.com/us/developer/docs/api/Content/field_types.htm#i1435915) needed to be [url encoded](http://www.w3schools.com/tags/ref_urlencode.asp) so that the report export could be directly imported into another system that couldn’t handle an un-encoded URL.

I would normally have handled that requirement with a formula field that called the [URLENCODE](http://www.salesforce.com/us/developer/docs/pages/Content/pages_variables_functions.htm) function that you have in Visualforce but it turns out that function isn’t available to you when defining a formula field.

So I had to resort to this rather terrifying use of the ‘SUBSTITUTE’ function in defining a new formula field. I thought I’d pass it on here for those who have similar needs.

```
SUBSTITUTE(SUBSTITUTE(SUBSTITUTE(SUBSTITUTE(SUBSTITUTE
(SUBSTITUTE(SUBSTITUTE(SUBSTITUTE(SUBSTITUTE(SUBSTITUTE
(SUBSTITUTE(SUBSTITUTE(SUBSTITUTE(SUBSTITUTE(SUBSTITUTE
(SUBSTITUTE(SUBSTITUTE(SUBSTITUTE(Custom_URL_Field__C, '!', 
'%21') , '#', '%23') , '$', '%24') , '&', '%26') , '\'', '%27') , '(', '%28'), ')', '%29') ,
 '*', '%2A') , '+', '%2B') , ',', '%2C') , '/', '%2F') , ':', '%3A') , ';', '%3B') 
, '=', '%3D') , '?', '%3F'), '@', '%40') , '[', '%5B') , ']', '%5D')
```

