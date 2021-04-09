+++
author = "Steven Herod"
date = 2011-08-29T00:00:00Z
description = ""
draft = false
slug = "vmforce-live-blog-"
title = "VMForce Live Blog."

+++


I’m putting together a ‘real’ app on VMForce + Heroku, I’m keeping an informal ‘live blog’ here :)

**Maven**

Maven, for some reason, failed to download ‘jdo-api-3.1’, so I manually downloaded using Chrome from here: [http://www.datanucleus.org/downloads/maven2/javax/jdo/jdo-api/3.1-SNAPSHOT-20110319/](http://www.datanucleus.org/downloads/maven2/javax/jdo/jdo-api/3.1-SNAPSHOT-20110319/) and installed it with:

```
C:\Users\sherod\Documents\workspace-sts-2.5.1.RELEASE>mvn install:install-file -DgroupId=javax.jdo -DartifactId=jdo-api -Dversion=3.1-SNAPSHOT-20110319 -Dpackag
ing=jar -Dfile=C:\Users\sherod\Downloads\jdo-api-3.1-SNAPSHOT-20110319.jar
```

**STS**

If you followed the instructions and only set your FORCE_FORCEDATABASE password details at the command prompt, then that’s not going to help STS.

```
C:\Users\sherod\Documents\workspace-sts-2.5.1.RELEASE>set FORCE_FORCEDATABASE_URL=force://test.salesforce.com;user=steven.herod@myapp.DEV;password=PasswordJJ$eZki3gEZTUIFrOZNz9adSs
```

After you’ve followed the setup instructions for STS to the letter, including the use of the vFabric tc Server, you should

1. Right click on your project
2. Select ‘Run As, then ‘Run Configurations…’
3. Select the VMware vFabric entry at the bottom of the list on the left, then click on its Environment tab:

{{< figure src="/images/downloaded_images/VMForce-Live-Blog-/0-nZasegaDWGVwlGl2.png" >}}

1. click Apply, then Run to run your server up with your new config.

**Consider changing your persistence.xml file if you are working with an existing Schema.**

Locate your persistence.xml file (src/main/resources/META-INF/) and change/add the values below in bold, lest you potentially make unintentional changes to your org.

```
<property name="datanucleus.autoCreateSchema" value="false" />
			<property name="datanucleus.autoCreateWarnOnError" value="false" />
```

**Oddities noted already**

The documentation page [here](http://forcedotcom.github.com/java-sdk/jpa-queries-soql) lists this code:

```
Query q = em.createNativeQuery(soqlQuery);
        // Bind the named parameter into the query
        q.setParameter("firstName", "Bob");
```

But if you run it you get: “javax.persistence.PersistenceException: Bind parameters not supported on native SOQL query”.That may be a config issue, but for now I’m hard coding parameters and will look into it further when I start to have to process user input.

**Getting it going on Heroku**

You are going to need Heroku set up (and git) which is kind of a big deal in and of itself, I’m not going to go into that now.

Configure your database/login details inside persistence.xml, by adding this line:

You need to follow steps 1 through 5 in this [blog entry](http://devcenter.heroku.com/articles/spring-mvc-hibernate), then skip to the section labelled ‘Declare Process Types With Foreman/Procfile’. Place your Procfile in your project’s home directory and make sure the case is right (I initially created it with Notepad and it was Procfile.txt, which doesn’t work obviously.

Follow your logs in a separate command window and from the projects home directory with ‘heroku logs -t’ to keep an eye on the logs.

This is all sketchy stuff, but I’m throwing it out there, if you aren’t previously familiar with mvn, heroku, git, JPA and SpringMVC its going to be very hard going. If I have time I’ll write up a more step by step setup. But for now, onwards to functionality.

**TC Server -> Not working after Heroku deployment.**

Sadly, getting it running it under jetty on heroku makes it incompatible with the tomcat setup on STS, you’ll need to comment out the additions to the pom.xml including jetty, and comment out Main.java before it runs again. I haven’t tried the ‘foreman’ inspired approach that the Heroku docs mention. Perhaps I can get it to run under tomcat on Heroku…. I’d prefer more rapid local development than a specific preference for Tomcat.

**OAuth**

I’ve reverted back to my local server and I’ve jumped right into OAuth following the instructions in the documentation. I’ve commented out the existing Security filter/filter mapping and added in the details from the documentation into web.xml like so:

```
<!-- Enables Spring Security -->
	<!-- <filter> <filter-name>springSecurityFilterChain</filter-name> <filter-class>org.springframework.web.filter.DelegatingFilterProxy</filter-class>
		</filter> -->
	<!-- <filter-mapping> <filter-name>springSecurityFilterChain</filter-name>
		<url-pattern>/*</url-pattern> </filter-mapping> -->

<!-- Enables Security -->
	<filter>
		<filter-name>AuthFilter</filter-name>
		<filter-class>com.force.sdk.oauth.AuthFilter</filter-class>
		<init-param>
			<param-name>connectionName</param-name>
			<param-value>forceDatabase</param-value>
		</init-param>
		<!-- Optional parameters -->
		<init-param>
			<param-name>securityContextStorageMethod</param-name>
			<param-value>cookie</param-value>
		</init-param>
		<!-- <init-param> <param-name>secure-key-file</param-name> <param-value>name
			Of Key-File</param-value> </init-param> -->
		<init-param>
			<param-name>storeUsername</param-name>
			<param-value>false</param-value>
		</init-param>

<!-- Optional parameters for logout configuration -->
		<init-param>
			<param-name>logoutFromDatabaseDotCom</param-name>
			<param-value>true</param-value>
		</init-param>
		<init-param>
			<param-name>logoutUrl</param-name>
			<param-value>/logout</param-value>
		</init-param>
	</filter>
	<filter-mapping>
		<filter-name>AuthFilter</filter-name>
		<url-pattern>/*</url-pattern>
	</filter-mapping>

The most important thing to remember is if you muck up your initial config at Salesforce for OAuth (i.e. put the wrong callback URL in) you need to delete that configuration and create a new one.  Whilst it lets you edit the url it won't actually ever work.  (As one would expect otherwise you could modify the URL after the inital setup and send calling apps somewhere bad).  Right now I've got a redirect happening from localhost to Salesforce, but I'm getting a '400' response on reply.   I'm investigating.

OAuth Continuing.

Hmm, not a 400. once I restarted everything it seems I have an infinite loop....  From localhost to SF to _auth/ back to SF....  Not sure why.  Which is a bug in the 22.0.3 version which they shipped.  According to the issue I raised here you need to use 22.0.5 or later (22.0.6 is the version I pulled and built from github).

Working with Entities.

Retrieving the records id field is mandatory in your SOQL query ([Select c.id from Custom_Object]), which is kind of logical given its the Entity ID that JPA will use.

Your classes which map to Custom objects need to drop the __c at the end, but maintain the underscore in their class name.  So 'Criteria_Finding__c' becomes 'public class Criteria_Finding'

If you change your class definition, you need to get the Data Nucleus stuff to 'do its magic' and can't rely on the auto-loading stuff to work.  I stop the built in tc Server, run 'Project -> Clean..', then start the server again.   If you just modify controllers or JSP files, you shouldn't need to do this, just save the change and wait for the server to reload the code.
```

