+++
author = "Steven Herod"
categories = ["deepdive", "developer", "architecture"]
date = 2017-07-01T00:00:00Z
description = ""
draft = false
image = "/images/downloaded_images/Salesforce-Platform-Events--a-quick-dive-into-EventBus-RetryableException/1-vdHl1-_Xk3y2fJG1FZhzdw-2.png"
slug = "salesforce-platform-events--a-quick-dive-into-eventbus-retryableexception"
summary = "\nIn Summer 17 Salesforce release the beta of what was, for me, a much awaited feature — Platform Events.\n"
tags = ["deepdive", "developer", "architecture"]
title = "Salesforce Platform Events, a quick dive into EventBus.RetryableException"

+++


In Summer 17 Salesforce release the beta of what was, for me, a much awaited feature — Platform Events.

To get a background on Platform Events you can check out [Trailhead](https://trailhead.salesforce.com/en/trails/force_com_dev_intermediate/modules/platform_events_basics) or for a more to the point explanation, the [Developer Guide](https://developer.salesforce.com/docs/atlas.en-us.platform_events.meta/platform_events/platform_events_intro.htm).

One of the interesting concepts in the documentation is mention of [EventBus.RetryableException](https://developer.salesforce.com/docs/atlas.en-us.platform_events.meta/platform_events/platform_events_subscribe_apex_refire.htm), which the documentation describes as:

> To retry the event trigger, throw EventBus.RetryableException. The event is resent after a small delay. The delay increases in subsequent retries…. You can run a trigger up to 10 times when it is retried (the initial run and 9 retries). After the trigger is retried 9 times, it moves to the error state and stops processing new events.

But what actually happens?

Since there is no ‘command centre’ for platform events the under-the-cover activity is a hard to figure out especially since I couldn't seem to get the system to produce debug logs.

So I figured I’d make use of Platform Events to figure out Platform Events.

I built a quick sample application which consisted of two Platform Events and a Custom Object.

{{< figure src="/images/downloaded_images/Salesforce-Platform-Events--a-quick-dive-into-EventBus-RetryableException/0-ZX0ua1kq5cBS6KFn.png" >}}

The basic concept was that:

1. I would publish an event to Test__e,
2. A trigger on Test__e would fire
3. This trigger would publish an event sending the number of retries that had occurred to Debug__e
4. The trigger on Test__e would then throw a EventBus.RetryableException.

```java
/*
 * Note, this isn't 'bulkified', whilst it looks like its running  one event, it could actually receive many events just like a trigger.
 * 
*/
trigger ResendEventsTrigger on Test__e (after insert) {
    
    Boolean quit = false;
    //Kill switch, to kill the event processing.
    for (Test__e t : trigger.new) {
          if (t.message__c == 'quit') {
              quit = true;
          }
    }

if (quit) {
       // do nothing
    } else {
        
        herod__Debug__e testEvent = new herod__Debug__e(retry_count__c = EventBus.TriggerContext.currentContext().retries);
        Database.SaveResult result = EventBus.publish(testEvent);
        throw new EventBus.RetryableException();
    }
}
```

Because Events are not rolled back when an exception occurs (unlike DML operations), the Debug Event survives the exception, is received in the Debug__e event listener which catches the event and creates a row in a custom logging object.

So, what’s the result?

The initial event is kicked off at 22.17:56 seconds

{{< figure src="/images/downloaded_images/Salesforce-Platform-Events--a-quick-dive-into-EventBus-RetryableException/1-CpJHYd0BAn3w9lnP8o-7-Q.png" >}}

2 seconds later the debug Event handler executes and inserts the first debug row with ‘Retry Count’ of 0.0

16 seconds later the system automatically retries to process the message and my code ensures the RetryException is thrown again.

{{< figure src="/images/downloaded_images/Salesforce-Platform-Events--a-quick-dive-into-EventBus-RetryableException/1-vdHl1-_Xk3y2fJG1FZhzdw.png" caption="Attempts logged grouped by retry frequency" >}}

The next 4 attempts occur at the 30 second intervals and the final 4 occur every minute until Salesforce ceases attempting to process the message on the 10th attempt.

Inside the Salesforce UI only the Event definition page shows signs of something having happened, with the ‘Subscription’ for the Trigger now showing a ‘Error’ state and a discrepancy between the ID of the last published event and the last processed event being 1 (the message we sent in test, having failed 10 times).

{{< figure src="/images/downloaded_images/Salesforce-Platform-Events--a-quick-dive-into-EventBus-RetryableException/1-LgB1y9LnTfwx7ZEKcEr7MQ.png" >}}

The trigger is now ‘dead’ in that it will not attempt to process any further messages. Re-sending messages will increase the ‘Latest Published Id’ number, but the trigger will not run.

{{< figure src="/images/downloaded_images/Salesforce-Platform-Events--a-quick-dive-into-EventBus-RetryableException/1-Za1JdqLoe3RMH1ev-tXNdA.png" >}}

Modifying the trigger (entering a space and quick saving) will return the trigger to a ‘running’ mode and it will re-attempt to process the backlog. Since I sent the kill message (containing the word ‘quit’) in one of the messages, my trigger exits successfully and is left in a ‘running’ state (which might be better described as ‘listening’).

{{< figure src="/images/downloaded_images/Salesforce-Platform-Events--a-quick-dive-into-EventBus-RetryableException/1-cZT1nxgcz682b-3lubo08Q.png" >}}

Note, that every invocation of a Event processing seems to consume an API Request, so 10 attempts is the equivalent of 10 API Requests. Something to keep in mind, especially in a development org.

Comments? Feedback? Your own Experiences, let me know!

