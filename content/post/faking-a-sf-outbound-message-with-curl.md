+++
author = "Steven Herod"
date = 2013-02-19T00:00:00Z
description = ""
draft = false
slug = "faking-a-sf-outbound-message-with-curl"
title = "Faking a SF Outbound Message with cURL"

+++


Recently I had an issue where a third party service which was receiving an outbound message was failing. Sadly Salesforce gives very little debugging information for outbound messaging if things go wrong (AFAIK you only get a single line in the Outbound Messaging monitoring list).

So, it can be handy to fake the outbound message sent from Salesforce to your test endpoint so you can get a bit more information.

Note, this is really only suitable for a test environment when you aren’t using sensitive data

I capture a version of my outbound message by setting up a PHP page that will simply email me the contents of the document posted to it and then pointing the outbound message configuration at that url temporarily.

Assuming you’ve saved that Outbound Message into a text file then is you can POST that file to your outbound message service using cURL to test how if is working and capture any error messages to Standard Out.

```
curl -X POST -d @outboundmessage.xml -H 'Content-type: text/xml' -H 'SOAPAction:\"notification"' http://test.example.com/web/service/url
```

