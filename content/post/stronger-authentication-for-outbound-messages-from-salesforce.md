+++
author = "Steven Herod"
date = 2013-03-27T00:00:00Z
description = ""
draft = false
slug = "stronger-authentication-for-outbound-messages-from-salesforce"
title = "Stronger Authentication for Outbound Messages from Salesforce"

+++


Salesforce offers a couple of mechanisms for securing Outbound messages.

Obviously the first step is to deploy your consuming web service to an SSL based end point and to use a CA signed certificate for the server.

You should also consider using your firewall to ensure that access to this endpoint is restricted only to the IP addresses which Salesforce uses for its services.

Finally you can also challenge Salesforce to provide a Client certificate to authenticate itself.

What you may not realise is that the client certificate is not unique to your organisation but rather generic to Salesforce.com

This opens the possibility of an outbound message being sent from another Salesforce organisation and malicious data being injected into whatever you have sitting behind your consuming webservice.

So what can you do about this?

**0. Remember the Organisation ID appears in the Outbound Message**

Every outbound message includes the ID of the organisation that sent it, verifying will assist you are receiving the message from the organisation you expected to receive it from. (thanks to [Stuart Hamilton](http://twitter.com/stuandgravy) for reminding me)

```
<element name="OrganizationId" type="ent:ID"/>
```

**1. Place a Token in the url.**

You could pass a token in the url of your configured endpoint:

[https://ws.example.com./soapendpoint?token=jklasfjklwenwer83h2820222423wfaf2dfasdf2](https://ws.example.com./soapendpoint?token=jklasfjklwenwer83h2820222423wfaf2dfasdf2)

Within the service that consumes the Outbound Message you could verify the token.

As long as you are using SSL the data in the URL should remain secret and this isn’t be any less secure than the rest of the data. The token will be visible to anyone with access to that configuration inside Salesforce.

**2. Verify Session ID**

You tick the box to receive the Session ID s part of the outbound message and by calling back to Salesforce’s identity service to verify the session and the identity of the session originator: [http://help.salesforce.com/help/doc/en/remoteaccess_using_openid.htm](http://help.salesforce.com/help/doc/en/remoteaccess_using_openid.htm)

This adds latency to the successful processing of the request.

**3. Pull**

Rather than transmitting all the information in the Outbound message send only the ID of the record then call back to SF with the session identifier (or with separate credentials) and conduct the query to retrieve the data. You may be doing this anyway in order to retrieve data related to the object which triggered the outbound message.

**4. Pass something in the object data**

Add a token as a field in the object and pass that over in the outbound message as data content. Probably not a great idea as it fills your data model with questionable data.

These are the options off the top of my head. Is there something I’ve missed or a secret sauce I’m not aware of? Let me know!

