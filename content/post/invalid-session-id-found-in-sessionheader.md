+++
author = "Steven Herod"
date = 2012-09-28T00:00:00Z
description = ""
draft = false
slug = "invalid-session-id-found-in-sessionheader"
title = "Invalid Session ID found in SessionHeader"

+++


Getting an error like this?

```
SFDC ERROR - INSERT TASK:INVALID_SESSION_ID: Invalid Session ID found in SessionHeader: Illegal Session. Session not found, missing session key: 00DN00000001xpU!ARkAQHV.1RXn.Nr34RSaEyGaq.yzqctjLmw.lpDKqzwFrVl15eE5bd85y4KfeSJzf.t6Z.2U3nNmbeduA71dEeg.607Tqk2M\n
```

Don’t worry, you have a valid session ID, but you’ve used it against an incorrect sandbox or Salesforce instance! I.e. You have executed a API login() call against test.salesforce.com and then on your subsequent call you’ve contacted cs5.salesforce.com instead of cs6.salesforce.com.

This change in pod usually occurs after a sandbox refresh (Salesforce often moves sandboxes between pods after a refresh). It can also occur with production instances after a pod split.

The best practice is to check the serverUrl field you receive in the [LoginResult](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_login_loginresult.htm#topic-title) response and to use this value as the URL in subsequent calls.

