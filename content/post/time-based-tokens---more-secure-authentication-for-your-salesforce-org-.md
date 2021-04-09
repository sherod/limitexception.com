+++
author = "Steven Herod"
date = 2014-08-16T00:00:00Z
description = ""
draft = false
slug = "time-based-tokens---more-secure-authentication-for-your-salesforce-org-"
title = "Time based tokens — More secure authentication for your Salesforce org."

+++


[caption id=”attachment_314" align=”alignright” width=”170"]

{{< figure src="/images/downloaded_images/Time-based-tokens---More-secure-authentication-for-your-Salesforce-org-/0-wQc8hNew-ce77NKV.png" >}}

Salesforce# app showing the random generated keys for two different Salesforce orgs and the countdown.[/caption]

Salesforce prides itself on the attention it pays to securing the platforms on which your Salesforce org sits — but that last mile which is your Salesforce org is in the hands of you and whomever you share your Salesforce administration duties with.

There are many, many facets to securing your Salesforce org, this blog post will cover only one aspect, a feature which arrived in the recent past but which I have seen few people adopt despite its benefits, that of ‘Time based tokens’ or ‘[Two Factor authentication](http://en.wikipedia.org/wiki/Multi-factor_authentication)’ (2FA for short).

Traditionally the first line of defence is an [excellent password](https://www.schneier.com/blog/archives/2014/03/choosing_secure_1.html), but I believe it should be standard practice for anyone who has administrative rights to your Salesforce org be required to use 2FA to enhance authentication.

2FA works on the principle of using two separate mechanisms to prove your identity to Salesforce. In the real world this is as simple as a Debit card and your debit card pin: Something you have (the card) and something you know (your pin).

In Salesforce’s world, these two factors are your traditional username & password and the use of a mobile application called ‘Salesforce #’ (available in the [iTunes App Store](https://itunes.apple.com/au/app/salesforce/id782057975?mt=8) and [Google Play](https://play.google.com/store/apps/details?id=com.salesforce.authenticator) stores).

Salesforce # a mobile application that produces a new random number every 30 seconds

[caption id=”attachment_316" align=”alignright” width=”300"]

{{< figure src="/images/downloaded_images/Time-based-tokens---More-secure-authentication-for-your-Salesforce-org-/0-qdJ_Z-xV7SJtjCpd.png" >}}

Physical RSA SecurID Token[/caption]

using (one assumes) a secure and unpredictable mechanism. This is identical to what you may already use with your Google account using [Google’s Authenticator](http://en.wikipedia.org/wiki/Google_Authenticator), or with a physical RSA SecurId token your employer may use.

Setting up your token generator (To be repeated for all users who will use it)

[caption id=”attachment_318" align=”alignright” width=”150"]

{{< figure src="/images/downloaded_images/Time-based-tokens---More-secure-authentication-for-your-Salesforce-org-/0-Z9GNU4Kca0Yz9RqY.png" >}}

User Detail page showing already setup time based token[/caption]

* Log into your Salesforce Org
* Go to your ‘User Detail’ page and locate the ‘Time-Based Token’ item
* Click ‘Add’
* Enter your username and password again
* Start your mobile app.
* Click ‘Add New key’
* Take a photo of the QR code.
* Done!

**From now on Salesforce will use this token to verify you when you login from an unknown computer (instead of emailing you the verification code).**

In order to get Salesforce to use 2FA on login, you need to add the use of Time-Based Tokens to your user.

If you are using a custom Profile, you can add this option in the ‘System Permissions’ section

[caption id=”attachment_313" align=”alignright” width=”860"]

{{< figure src="/images/downloaded_images/Time-based-tokens---More-secure-authentication-for-your-Salesforce-org-/0-rk8W1J4xPO6OQNmn.png" >}}

Enabled permission in ‘System Permissions’[/caption]

However, I prefer to use a Permission Set to do this.

1. Create a new Permission Set called ‘Two-Factor Authentication’
2. Tick the ‘Two-Factor Authentication for User Interface Logins’ in the ‘System Permissions’ section
3. Save the Permission Set
4. **Make sure everyone who is going to be affected knows about the change! (See below)**
5. Add the Permission Set to all users with System Administrator profile (or any other profile with sensitive rights).

Now when you login you’ll see the traditional login screen, and then after you are successful with your username and password, you’ll see this screen.

[caption id=”attachment_315" align=”aligncenter” width=”300"]

{{< figure src="/images/downloaded_images/Time-based-tokens---More-secure-authentication-for-your-Salesforce-org-/0-9KX5c2e3v0Jsaat4.png" >}}

2FA code verification screen[/caption]

Time to find where you left your phone!

### Questions

**What happens if the people assigned the permission set haven’t setup their time based token?**

They’ll need to install the app, when they login they’ll get a screen like below:

[caption id=”attachment_321" align=”aligncenter” width=”300"]

{{< figure src="/images/downloaded_images/Time-based-tokens---More-secure-authentication-for-your-Salesforce-org-/0-Cxqq2zSyXawUHKiy.png" >}}

What someone sees on login if they haven’t set up a token but their config requires it.[/caption]

**What happens if I delete the app by mistake?**

On the iPhone at least, reinstalling it from the app store will recover your 2FA setup without any issues.

**What happens if I delete the token configuration on my phone?**

You can remove the token setup by swiping it and deleting it, if its gone you’ll need another Administrator to remove your time based token on your User record to allow you to set it up again on your next login. **It’s probably a good idea to have at least two Administrators configured for your org!**

