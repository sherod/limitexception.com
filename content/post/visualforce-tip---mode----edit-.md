+++
author = "Steven Herod"
date = 2013-09-10T00:00:00Z
description = ""
draft = false
image = "https://images.unsplash.com/photo-1575538031230-3e9ebd2fd631?ixlib=rb-1.2.1&q=80&fm=jpg&crop=entropy&cs=tinysrgb&w=2000&fit=max&ixid=eyJhcHBfaWQiOjExNzczfQ"
slug = "visualforce-tip---mode----edit-"
title = "Visualforce tip — mode = ‘edit’"

+++


Quick trivial reminder about a small attribute that has quite a visual impact on how your edit page looks in Salesforce / Visualforce

With

```
<apex:pageBlock title="Site Certification Standard Edit" mode="edit">
```

Without

```
<apex:pageBlock title="Site Certification Standard Edit”>
```

As you can see, the page looks more like the normal Salesforce edit layout, complete with the ‘Red bar’ hint.

