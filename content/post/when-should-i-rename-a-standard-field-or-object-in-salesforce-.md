+++
author = "Steven Herod"
date = 2020-09-26T11:42:16Z
description = ""
draft = true
slug = "when-should-i-rename-a-standard-field-or-object-in-salesforce-"
summary = "\nAlmost never.\n"
title = "When should I rename a standard field or object in Salesforce?"

+++




## Almost never.

I use ‘almost’ because there is always an exception, but in general, renaming standard fields and objects turns out to be a problem as your org grows and changes from solving the specific problem you renamed the item for, to a more general solution for your business.

Renaming standard fields/objects/tabs is one of those changes you have to make that is org wide, meaning all subsequent users of the system must use the new custom language.

When your org is young and in use by a single department/team, this can mean you can tailor Salesforce to provide very specific language, at the cost of handling more generic circumstances. You are faced with two choices, carrying the custom language into the new project and incurring the cost of it not being aligned with a general usage, or going back and reworking your existing solution (and documentation, and users) to the new language.

Now, there are a number of cases where an organisation’s purpose and nature is so strong that the use of new language is essential, but if that's not the opinion of the entire organisation, you should only take this step

