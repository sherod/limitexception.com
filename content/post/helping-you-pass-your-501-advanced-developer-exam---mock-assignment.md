+++
author = "Steven Herod"
date = 2011-12-14T00:00:00Z
description = ""
draft = false
slug = "helping-you-pass-your-501-advanced-developer-exam---mock-assignment"
title = "Helping you pass your 501 Advanced Developer Exam / Mock Assignment"

+++


```
Note, this blog entry has been revised as at Nov 10 2014 to 
include a different webservice and clearer requirements.
```

The purpose of this blog entry is to describe a contrived business problem that exercises the topics covered in the 501 Developer exam.

**Problem**You are the founder and CTO of your own company, WeatherForce.com and you have, for reasons known only to yourself, concluded that there is a market for a weather service which people interact with via email.

**Email Handling**

* A customerwill email a weather enquiry to your Developer Edition Organisation and receive a short while later a reply ocntaining the details of the weather for the location they specified in the subject line.
* You will need to develop several components to handle this.
* You will need to write an ‘inbound email handler’ which:
* Receives the incoming email, saving its subject and body to a custom object that you will create.
* Get the email ‘From Address’ and check whether that particular sender is a Contact in the organisation, if it isn’t, create a contact.
* You will need to write a trigger on your Custom Object
* When the subject and body are saved, an insert trigger (experiment with before and after) will run which conducts a search of this weather service (http://www.webservicex.com/ws/WSDetails.aspx?CATID=12&WSID=56) using the SOAP API described at the following WSDL (http://www.webservicex.net/globalweather.asmx?WSDL)
* You **must conduct the web service call from the Trigger.**
* You will store the response into a master detail record of the search by checking whether there exist a search query similar to that in the org, if there exist then the results in the response should be merged to the existing detail record of the search.
* Using Batch Apex and Scheduling you will then compose response emails using a Visualforce template which emails the search results back to the originating user. Also attach a PDF of the results to the email you send.

**Visualforce**

* Internal staff at your company want to use a web browser to look up the weather. Develop a Visualforce page that:
* Shows the weather search history and when you clicks on a search record, will show the weather results inline without moving to a new web page.. (Hint: Add an ActionSupport and ReRender)
* Add actionStatus to make the user aware that the data is loading.
* Make sure the page adopts the styling of the Account tab.
* After completing this build, move the Visualforce elements you created on the page to a custom component and re-write this page to use the custom component.
* Refactor your work to use a custom class (not sObject) wrapper for the search results, consisting of inner and outer classes.
* Add page footer for the page using Visualforce Template features.
* Experiment with the effect of adding and removing the search results from the view state.

**Deployment**

* Register a second Developer organisation.
* Migrate your package between your first developer organisation and your second using only the Force.com IDE.

**Tests**

* Write tests to exercise the ALL the above functionality, aim for over 75% coverage, including the call to the Weather Web service and inbound and outbound email services. Ensure that some or all of these tests run as two different types of user.

**Documentation**

* Create a [sequence diagram](http://en.wikipedia.org/wiki/Sequence_diagram) explaining the order of execution and sequence of interactions between the controller/extensions/custom components / etc
* Create a [sequence diagram](http://en.wikipedia.org/wiki/Sequence_diagram) explaining the execution order of your trigger.

