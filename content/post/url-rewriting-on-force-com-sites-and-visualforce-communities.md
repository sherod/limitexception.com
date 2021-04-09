+++
author = "Steven Herod"
date = 2016-08-20T00:00:00Z
description = ""
draft = false
image = "https://images.unsplash.com/photo-1518674660708-0e2c0473e68e?ixlib=rb-1.2.1&q=80&fm=jpg&crop=entropy&cs=tinysrgb&w=2000&fit=max&ixid=eyJhcHBfaWQiOjExNzczfQ"
slug = "url-rewriting-on-force-com-sites-and-visualforce-communities"
title = "URL Rewriting on Force.com Sites and Visualforce Communities"

+++


Salesforce has for some years supported URL Rewriting to allow friendly URLs in force.com sites and Visualforce communities, that is, instead of ‘https://community.example.com/apex/Page?id=a000000000001' you can have friendly URL like ‘https://community.example.com/product/acme-best-chicken-gravy'.

**It’s also essential to note that when you create a Visualforce/Tab community the standard Salesforce UI still lurks beneath your custom User Interface, so make sure your Profile security is 100% correct, additionally this advice is only applicable to Visualforce based Communities, URL rewriting is not available using the Lightning Community Templates.**

There are some interesting aspects of this capability however you should be aware of.

### Order of evaluation

Your URL Rewriter is not the first thing to handle URL requests, in fact, its about the third thing to kick in. From my experimentation the order of priority for URL interception is:

1. The URL Redirects configuration section of the Site
2. Salesforce standard interceptor for record ids
3. Your URL Rewriter Class
4. Misc other standard URLs (chatter, search, files, admin pages etc)

The rest of this article will discuss the specifics of these functions.

### 1. URL Redirects

This is a configuration option off the Site setup, here you can override specific URLs (i.e. no wildcards) and redirect them to other locations; including locations you might further rewrite. In this example the route /logout has been re-written to the standard Salesforce logout jsp, access to the Contacts list view and standard Home Page have been removed.

{{< figure src="/images/downloaded_images/URL-Rewriting-on-Force-com-Sites-and-Visualforce-Communities/0-FqZOy5YpdZY45liq.png" >}}

{{< figure src="/images/downloaded_images/URL-Rewriting-on-Force-com-Sites-and-Visualforce-Communities/0-Ez91pNzUdYsQb5xu.png" >}}

### 2. Object ID handler

Any URL which contains a Salesforce Object ID will not work, instead Salesforce’s standard UI will kick in and take control, so if you have a URL like

✘/routeto/a00N000000E23Zs

Salesforce is going to kick in and take that request, sending it to the standard page handler before it gets to your re-writer. The solution is to avoid using IDs or to disguise them.

Prefixing them with another character is more than sufficient, this can be removed when you process the URL in your class

E.g.

**✓** /routeto/ka00N000000E23Zs

### 3. Your URL Rewriter

The [URL Rewriter](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_site_urlRewriter.htm) implements the [Site.UrlRewriter](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_site_urlRewriter_reference.htm#apex_site_urlRewriter_reference) interface, you’ll notice if you look at the documentation that there are a number of reserved words which you cannot use so when designing your clean URL scheme keep these limitations in mind. One of the most important I’ve found is the fact a fullstop ‘.’ is prohibited, so a profile page that uses community id as the url with a full stop in it will not work

✘ /profile/steven.herod

**✓** /profile/steven_herod

### Writing the URL

This class deserves to be well written as it can be the source of some interesting bugs. Your creativity with intercepting various routes is really down to your ability to do string matching and parsing. What I found was you have a class ‘if / then’ statements which go through four stages:

1. Initially match the URL using one of the [String ‘startsWith’ or ‘contains’ methods](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_methods_system_string.htm)
2. Undertake a URL parsing approach specific to that route (using split or subString)
3. Look up the destination (using data extracting from a URL in a SOQL query to locate records).
4. Return a PageReference to the destination page, after setting the parameters used by that page.

e.g:

```
//Match the url
if(url.startsWith(ROUTE_USERPROFILE)){
   String id;
   PageReference p = Page.Profile;
// Parse the path
   String name = url.substring(ROUTE_USERPROFILE.length(), url.length());
    if (!String.isEmpty(name)) {
//Lookup the destination
        id = [select id from User where CommunityNickname = :name limit 1].id;
        p.getParameters().put('id',id);
    }
//Return the PageReference
    return p
}
```

### Things to keep in mind

1. Process the routes in the order of priority (e.g. you’ll want to match ‘/profiles’ before ‘/profile’ if you use startsWith()).
2. You have no access to [UserInfo.xx](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_methods_system_userinfo.htm) etc to figure out who the user is, so routes need to be generic, if you need to do user based routing best to bounce the user off a Visualforce page which does have access and can redirect it to a user/profile specific page.
3. Keep in mind you are accepting arbitrary information from a potentially malicious user, either use bind variables or other steps to avoid [SOQL injection attacks](https://developer.salesforce.com/docs/atlas.en-us.pages.meta/pages/pages_security_tips_soql_injection.htm)

* This is NOT A SECURITY TOOL, using URL Rewriter as the mechanism to secure your site is futile, you can use it to ‘hide’ places end users probably shouldn’t poke around, but your only guarantee of security is removing Object level and Field Level access at the Profile level, your Sharing Model, and configuration of Tabs/List Views and Home Page Layouts.

1. Its a great way to break your site (minor errors can result in the site becoming unavailable).

### Other standard URLs

When I first setup the URLRewriter I was fairly aggressive, when a route didn’t match one of the ones I’d configured I was sending people to a /home URL. This resulted in much of the community administration of the site no longer working as these standard URLs were being processed after URL Rewriters, as I mention above restricting access to some of these URLs can be helpful to hide portions of standard functionality, but its not a cast iron security stem.

