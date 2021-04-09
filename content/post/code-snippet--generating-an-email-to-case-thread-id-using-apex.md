+++
author = "Steven Herod"
date = 2013-06-22T00:00:00Z
description = ""
draft = false
image = "https://images.unsplash.com/photo-1547042591-aae98619aab5?ixlib=rb-1.2.1&q=80&fm=jpg&crop=entropy&cs=tinysrgb&w=2000&fit=max&ixid=eyJhcHBfaWQiOjExNzczfQ"
slug = "code-snippet--generating-an-email-to-case-thread-id-using-apex"
title = "Code Snippet: Generating an Email-to-Case thread id using Apex"

+++


A quick Saturday morning code snippet from something I wrote this week.

Here’s how to generate an Email-To-Case thread ID for insertion into an email body or subject line.

You’ll need to pass in the id of the Case you want replies threaded to.

```
private String getThreadId(String caseId){
 return '[ ref:_' 
         + UserInfo.getOrganizationId().left(4) 
         + '0' 
         + UserInfo.getOrganizationId().mid(11,4) + '._' 
         + caseId.left(4) + '0' 
         + caseId.mid(10,5) + ':ref ]';
 }
```

