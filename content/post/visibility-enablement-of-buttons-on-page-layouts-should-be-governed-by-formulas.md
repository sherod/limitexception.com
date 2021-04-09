+++
author = "Steven Herod"
date = 2012-03-06T00:00:00Z
description = ""
draft = false
slug = "visibility-enablement-of-buttons-on-page-layouts-should-be-governed-by-formulas"
title = "Visibility/Enablement of Buttons on page layouts should be governed by formulas"

+++


On many page layouts I often have the need to place custom buttons and often these buttons are only valid in certain contexts, for instance, one should only be able to submit the data to an external service IF the data has a status of ‘Open’.

Currently I have only four undesirable choices…

1. Replace the page layout with a custom visualforce page
2. Place a guard on the target of the button to tell the user “You can’t do that because of x”
3. Change the record type of the object and then have a custom page layout for that record type.
4. Inject Javascript into the sidebar that modifies the dom/html to hide/disable the button.

All of these options inelegant or potentially dangerous.

What I would like is the ability that when placing a button on a page layout I can define a formula field which decides if the button is visible or invisible (and enabled or disabled).

This would solve major usability issues on ALL of the force.com application development I’ve undertaken in the past 18 months.

I’ve logged [this idea in the idea exchange](https://sites.secure.force.com/success/ideaView?id=08730000000gl64AAA), if you agree with it, please, please upvote it.

