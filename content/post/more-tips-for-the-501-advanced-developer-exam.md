+++
author = "Steven Herod"
date = 2011-12-19T00:00:00Z
description = ""
draft = false
slug = "more-tips-for-the-501-advanced-developer-exam"
title = "More Tips for the 501 Advanced Developer Exam"

+++


The exam contains a lot of ambiguous questions and things like ‘Pick which of the three below are right, Which what is NOT true’.

I remain unconvinced you can cram for it without having done a fair amount of real force.com development, normal force.com development and deployment should be something you ‘just know’ before cramming the specifics.

Topics covered

* Custom components, syntax for declaring and usage.
* Templating, syntax for declaring and usage.
* Page life cycle, order of controller, action and getter/setter execution <- multiple questions.
* isTest and its requirements for class visibility, impact on governor limits and what is valid for them to contain.
* Things you can to do to improve test coverage.
* Constructors, are they needed, can they be overloaded?
* What coding constructs are valid to bind Visualforce components to (sObjects, Custom Classes and their members, Inner classes)
* How you reference component ID’s using $Component
* Static Resources, benefits over Documents, limits and syntax for how they are accessed
* When to use a Full Copy sandbox, when to use a Developer Edition.
* URL and username convention for Sandboxes (Production and DEveloper Edition vs all other types)
* Purpose of Code Share
* What tools can use the metadata api (Force.com IDE, Migration tool)
* How to test inbound email handlers, what one needs to do to handle inbound email.
* What tags are mandatory in Visualforce Email templates, when can they be used (i.e. not Mass email).
* What package specific methods are in (System vs Test vs ApexPages vs )
* Purposes of Governor limits (Specifically number of script lines executed)
* How to get a Visualforce page into your solution (overriding buttons, lists in page layouts, by URL).
* How to get / set HTTP parameters with a PageReference, how to get a Page Reference.
* What happens with Triggers when you merge or Undelete records, especially the CRM records (Accounts).
* Order of trigger execution -> multiple questions from putting 6 things in the right order to nuances between ‘saving’ a record and committing a record.
* How to recognize Dynamic SOSL, SOQL, DescribeResults and Token methods.
* What files get created with the migration tool (package.xml, destructiveChanges.xml, files describing the object.)
* Outbound messaging, what the contents are of its payload.
* When you can use call outs, how triggers and callouts interact
* Entry point for code from tests, does calling a webservice method from a test run in test or webservice context?
* startTest and stopTest, meanings, when to use it.
* When to use Apex and Visualforce.
* What’s the best way to move changes between developers working together, as an ISV, or as releasing software internally.

