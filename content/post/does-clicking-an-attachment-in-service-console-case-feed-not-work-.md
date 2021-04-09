+++
author = "Steven Herod"
date = 2014-12-13T00:00:00Z
description = ""
draft = false
slug = "does-clicking-an-attachment-in-service-console-case-feed-not-work-"
title = "Does clicking an attachment in Service Console Case Feed not work?"

+++


If you are currently experiencing the following problem:

1. You have Enabled ‘My Domain’
2. You are using the Service Console
3. You have turned on Case Feed
4. You are using its ‘Compact Layout’ feature

And

1. Clicking on email attachments in the case feed results in nothing happening.

Then you might think you are experiencing this [‘Known Issue’](https://success.salesforce.com/issues_view?id=a1p30000000eJaFAAU): I know I did.

Turns out this appears to be an issue with configuration that doesn’t happen automatically.

The way to fix it is:

1. Turn on your Javascript Console in your fav browser (I use Chrome).
2. Click the link, you’ll see a message appear in the log:

{{< figure src="/images/downloaded_images/Does-clicking-an-attachment-in-Service-Console-Case-Feed-not-work-/0-B-9sMAzzExt2w9B6.png" >}}

You might recognise this as the problem you have with other URL in the service console, you need to white list it.

To do this,

1. Go to Setup
2. Click ‘Apps’
3. Select your Service Console app from the list.
4. Click ‘Edit’
5. Add the domain mentioned in your error message to the whitelist section. In my case it was ‘herod-dev-ed — c.na12.content.force.com’.
6. Click Save
7. Refresh the Service Console page in the browser.

{{< figure src="/images/downloaded_images/Does-clicking-an-attachment-in-Service-Console-Case-Feed-not-work-/0-d0JmgGcCcrMEbNNo.png" >}}

The problem should be eliminated.

