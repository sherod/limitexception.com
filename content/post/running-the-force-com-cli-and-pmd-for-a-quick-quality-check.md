+++
author = "Steven Herod"
categories = ["developer", "howto"]
date = 2017-09-26T00:00:00Z
description = ""
draft = false
image = "https://images.unsplash.com/photo-1578255783478-a86ff94321b0?ixlib=rb-1.2.1&q=80&fm=jpg&crop=entropy&cs=tinysrgb&w=2000&fit=max&ixid=eyJhcHBfaWQiOjExNzczfQ"
slug = "running-the-force-com-cli-and-pmd-for-a-quick-quality-check"
summary = "\nInstall the force.com CLI, confirm it runs from your current working directory by running ‘force’\n"
tags = ["developer", "howto"]
title = "Running the Force.com CLI and PMD for a quick quality check"

+++


1. [Install the force.com CLI](https://developer.salesforce.com/tools/forcecli), confirm it runs from your current working directory by running ‘force’
2. [Install PMD](https://pmd.github.io/pmd-5.8.1/usage/installing.html), confirm it runs from your current working directory by running PMD

Then, run the following commands in sequence

```
cd <target directory>
mkdir metadata
force login
force export ApexClass
pmd -d metadata\classes -R rulesets/apex/ruleset.xml -f html -reportfile report.html
report.html 
```

I then cut and paste the report.html contents from browser to Excel for subsequent review and processing.

