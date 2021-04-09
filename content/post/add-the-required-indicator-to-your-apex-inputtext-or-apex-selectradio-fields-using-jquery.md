+++
author = "Steven Herod"
date = 2012-03-16T00:00:00Z
description = ""
draft = false
slug = "add-the-required-indicator-to-your-apex-inputtext-or-apex-selectradio-fields-using-jquery"
title = "Add the required indicator to your apex:inputText or apex:SelectRadio fields using jQuery"

+++


One of the frustrating aspects of salesforce is some of the UI element generation it does (and in this case, doesn’t do) for you.

While <apex:inputField required=”true”> will add the standard salesforce required indicator (the red bar) to your page with no further effort, if you have to drop down to the lower level <apex:inputText required=”true”> tag, you’ll miss out on this help, leaving you to wrap your inputText field in various chunks of HTML in order to have Salesforce’s standard stylesheets into apply the appropriate look.

Recently I had this requirement on several text fields and a selectOption field and rather than inject lots of HTML into my VF page manually I decided to use jQuery to help me out.

First, I defined my inputText with an additional class of ‘requiredIndicator’, this is just a marker so the text field (and any others with the same class on the page) can be found by jQuery.

```
<apex:inputText label="{!$ObjectType.Account.fields.name.label}" required="true" styleClass="requiredIndicator"  value="{!form.AccountName}" />
```

Next came the jQuery (in this case I’m using a jQuery bundle I’ve previously added to the static resources)

```
<apex:includeScript value="{!URLFOR($Resource.jQueryForce,'/js/jquery-1.6.4.min.js')}" />

<script type="text/javascript">
	   $(function(){
	  		$('.requiredIndicator').wrap('<div class="requiredInput">').before('<div class="requiredBlock"></div>');
	  	}
	   );
  </script>
And here is the end result (all of these fields are inputText):

It also works with selectOptions, which also don't show required indicators:

<apex:selectRadio value="{!stockOption}" required="true" label="Stock Availability" styleClass="requiredIndicator"> 
   <apex:selectOption itemValue="vehicleInStock" itemLabel="{!$ObjectType.PricingRequest__c.fields.VehicleInStock__c.label}"/>                    
   <apex:selectOption itemValue="dealerSwapRequired" itemLabel="{!$ObjectType.PricingRequest__c.fields.DealerSwapRequired__c.label}"/>
   <apex:selectOption itemValue="poolStock" itemLabel="{!$ObjectType.PricingRequest__c.fields.PoolStock__c.label}"/> 
   <apex:selectOption itemValue="factoryOrder" itemLabel="{!$ObjectType.PricingRequest__c.fields.FactoryOrder__c.label}"/> 
</apex:selectRadio>

Check the jQuery site to read more on class selector and the wrap and before methods
```

