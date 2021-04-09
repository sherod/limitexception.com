+++
author = "Steven Herod"
categories = ["productivity"]
date = 2020-10-11T03:44:46Z
description = ""
draft = false
image = "https://images.unsplash.com/photo-1557568192-387504499261?ixlib=rb-1.2.1&q=80&fm=jpg&crop=entropy&cs=tinysrgb&w=2000&fit=max&ixid=eyJhcHBfaWQiOjExNzczfQ"
slug = "protonmail"
tags = ["productivity"]
title = "Protonmail - A Review"

+++


As part of my [new personal tech stack](/using-aws-for-personal-networking/) I've switched my personal email from Gmail to Protonmail, I thought I'd outline a few impressions after a few weeks of usage.

### What is Protonmail?

Protonmail offers 'secure' email, in that its hosted in Switzerland, and uses 'zero access' encryption to protect my mail.  What this means is that my email is held at rest in an encrypted form (like Salesforce Platform Encryption), and it only decrypted when it is accessed with my customer specific encryption key.  As a result, the providers of Protonmail have no access to my email.

### As a secure experience

Protonmail collects very little information about you in order to offer you an email service, this anonymity can be of value, although, given I tied it to a domain name based on my surname, of little value to me personally.

All logins require multi-factor authentication, given that the most likely way of being compromised is my own login credentials, this is essential.

The encrypted at rest email is safe from being read even if the core service is penetrated, although, if a total compromise were to occur, this could still be beaten - and despite the encryption at rest, you email still crosses the open internet (Albeit, over TLS).   Only Protonmail to Protonmail is fully encrypted, but that honestly is no different to Whatsapp.

At the end of the day, do you trust Google with all its capabilities to keep your email safe, or a small dedicated team of techies in a stand alone service? It can be hard to quantify that.

### As an email experience

There's no doubt, that despite what Protonmail says about security, its worse at spam filtering than Google is.   I've had a handful of messages, one fairly convincing at phishing, turn up in my inbox, whilst legitimate emails have been filtered to spam.

So you will spend a little more time dealing with this.

The secure nature also means a few other things:

1. You have to use their iPhone and Android clients, you can't use third party email apps with Protonmail.  I would describe the iPhone app as 'workman like'.  It does the job, but you'll not necessarily have a delightful experience.
2. There's no persistent login on the web client.  So logging in will require username/password and your multi-factor code on each login.  This is obviously a security choice, but worth knowing.
3. The web client is otherwise fine and seems to work well.

Finally, no ads.  Given Protonmail is a paid service, you avoid the ads, a benefit I do enjoy immensely.

### Final thoughts.

I'm not sure I'd recommend Protonmail for the general public, but if you are security conscious technical person, it's got strong credentials and its a reasonable email experience.

