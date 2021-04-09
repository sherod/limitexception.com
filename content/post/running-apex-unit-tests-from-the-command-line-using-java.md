+++
author = "Steven Herod"
date = 2012-08-13T00:00:00Z
description = ""
draft = false
slug = "running-apex-unit-tests-from-the-command-line-using-java"
title = "Running Apex unit tests from the command line using Java"

+++


Below is a simple program I created that uses the Salesforce APIs to execute a list of unit test class names passed as arguments from the command line.

To reproduce this work you will need the [web services connector wsc.jar file](http://code.google.com/p/sfdc-wsc/downloads/list), your Enterprise WSDL file and your Apex WSDL from your Salesforce organisation.

First, use the wsc to generate your client side code:

```
java -classpath wsc-22.jar com.sforce.ws.tools.wsdlc enterprise.wsdl enterprise.jar

java -classpath wsc-22.jar com.sforce.ws.tools.wsdlc apex.wsdl apex.jar
```

Then, place the apex.jar and enterprise.jar files into your Java project’s classpath

Then use the code below, substituting the correct username, password+token and SF instance (ap1, cs5 etc).

[gist id=3340160]

This is also now on github as a project: [https://github.com/sherod/SalesforceTestRunner](https://github.com/sherod/SalesforceTestRunner)

