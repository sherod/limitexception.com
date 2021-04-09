+++
author = "Steven Herod"
categories = ["architecture"]
date = 2018-11-28T00:00:00Z
description = ""
draft = false
image = "/images/2020/09/elle-hughes-sFU3-fwZ6nQ-unsplash-2.jpg"
slug = "-hot--objects---salesforce-at-scale"
tags = ["architecture"]
title = "‘Hot’ objects — Salesforce at Scale"

+++


Every large scale Salesforce instance has certain objects in its data model which are heavily utilized.

Such ‘heavy’ utilization has several forms. It may involve a considerable number of fields (> 500 plus), a large number of records (tens of millions), or a large amount of automation (Process Builder, Triggers, etc).

These objects are problematic in that in interacting with them is inherently challenging. Changes to the manner in which they are accessed (i.e. a sudden increase in record insertion) may uncover performance problems, or new functionality may exhaust available capacity (another validation rule, one more lookup field).

This typically results in the need to rework existing functionality in new approaches, such as splitting fields onto new objects or moving from Process Builder to apex triggers. Whilst some of this can be avoided with careful design and best practices the reality is that changing business needs can cause previous solutions to become invalid.

These challenges can come as a surprise, either at analysis time or, worst case, at runtime when limit exceptions are thrown.

To avoid this I’m suggesting the term ‘Hot’ be used to define objects which are proven to have issues or which potentially could have issues based on analysis and experience. A ‘Hot Object’ could be called out in design documentation or within the description of the Object on the platform, indicating to teams working on them that this object requires a heightened level of design and change effort.

Dealing with ‘Hot Objects’ could be factored into design and governance sessions, so that ongoing maintenance and enhancement activities can be structured to ‘turn down the heat’, by refactoring solutions to remove these stressors.

Thoughts?

