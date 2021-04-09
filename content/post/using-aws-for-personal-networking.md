+++
author = "Steven Herod"
categories = ["deepdive"]
date = 2020-10-01T13:13:11Z
description = ""
draft = false
image = "https://images.unsplash.com/photo-1520869562399-e772f042f422?ixlib=rb-1.2.1&q=80&fm=jpg&crop=entropy&cs=tinysrgb&w=2000&fit=max&ixid=eyJhcHBfaWQiOjExNzczfQ"
slug = "using-aws-for-personal-networking"
tags = ["deepdive"]
title = "Professional Development with AWS"

+++


### The History

For 21 years I've hosted my personal website and miscellaneous experiments on [Dreamhost](/using-aws-for-personal-networking/dreamhost.com).

Dreamhost was where I first setup my  website.  My sites and content there have survived countless life milestones.  I started out hosting private projects in HTML built in Microsoft Frontpage, [HotDog](https://en.wikipedia.org/wiki/HotDog), [Macromedia Dreamweaver](https://en.wikipedia.org/wiki/Adobe_Dreamweaver).  From then I moved on to teaching myself PHP, building basic content management systems before the days of Wordpress.

For many, many years it languished.  It was occasionally in use when I needed to dump a quick experiment up on the site.  It was a useful endpoint for debugging outbound messages in Salesforce and a place to setup domains for ideas I never finished.   During my Ruby on Rails experimentation it was frustrating, Rails never ran well on the shared hosting, and whilst I toyed with virtual machines and Ruby specific hosting, it never got too serious, I always came back to Dreamhost.

But in the last few years I've started to think further professional development, and the obvious candidate is Amazon Web Services.  So with the goal of learning more I started the process of moving out of Dreamhost and on to AWS.

### The Old Topology

{{< figure src="/images/2020/10/Team-Structure--1-.png" caption="The old approach, with Dreamhost." >}}

I have had several approaches to web hosting over the years, starting with Static HTML and moving to Wordpress hosted with the aid of Dreamhost's free SQL servers.  When Medium became popular, and tired of the constant Wordpress upgrades, I decided to migrate this blog to Medium, leaving behind a blank page on herod.net.  Email has been mainly running on Google with a vanity domain and mail forwarding from Dreamhost.  All of this has been held together with DNS hosted on at Dreamhost.

### The New Way

This approach is based on a exploring as many AWS technologies as possible, so, for a blog that gets around 12 visitors a day, this is frankly overkill, and I should point out, much, much more expensive.

{{< figure src="/images/2020/10/0_0.png" caption="The new, much more complicated way" >}}

As you can see from the diagram, DNS has been moved to Route 53.  I'd known the name, but not really looked at it, so I was surprised to find it quite easy to use.  For various reasons I couldn't have ProtonMail handle the mail directly, so I had to use email forwarding to get my email to them.  The challenge is Route53 doesn't do email forwarding, just MX records, so I needed something to fill that gap - so I turned to Improv.mx, a free email forwarding service, coupled with ProtonMail for secure email.

The next step was a CMS for the blog and other websites.  I'd previously been dissatisfied with Wordpress, so I looked for an alternative. I turned to Ghost.  A modern and simple CMS with some attractive templates.

But how to host it?  I tossed up running Lightsail, but I wanted to get a little closer to the raw services, so went with ec2.

My EC2 instance is a t2.micro running Ubuntu, with Nginx doing the SSL stuff (via [LetsEncrypt](https://letsencrypt.org/)) and reverse proxying to Node.js running Ghost.   Database services are a dedicated Aurora Database (in MySQL compatibility Mode) on [RDS](https://aws.amazon.com/rds/).

The whole process took probably about 8 hours from start to finish in terms of work, including importing historical blog posts.  The most challenging process had been the DNS transition and some of the multi-site hosting approaches used by Nginx and Ghost

### Conclusion

This has been a fun little project, I've learned a bit and gotten to see what the state is of running these services. To be honest, I was quite impressed.  Given my previous experiences with Linux and service, this was a far more user friendly process.

### Extra Credit

Now I have a web server in Ohio on a t2.micro, a RDS database and some DNS, but what more could I do?

How about [pi-hole](https://pi-hole.net/)?

I had previously run this on my home LAN on my trusty [Kogan NUC](https://www.kogan.com/au/buy/kogan-atlas-e300-s-mini-pc-windows-10-pro/), but I found it to not be particularly quick.  But what could the cloud do:  So I installed it on another EC2 instance in Ohio, with a second one running in Sydney.   It's been up and running now for a couple of days, and the ad-free internet is a blissful pleasure.     It remains to be seen if I will keep this up, I'm a little concerned about the cost, and the security.  Pi-hole normally lives safely on your local LAN, whilst I've taken the security precaution with AWS Security Groups to restrict its access to my home static IP address, I feel like more is needed.

### Whats next?

I've got a to do list to cross off a few more things, but in the immediate term its:

* Making the network reliable, with the appropriate CloudWatch options.
* Making sure backup of the database and the ec2 instances.
* Load balancing (Although, really only to experiment).
* Lamba's and all the dev related stuff.

Thanks for reading, any comments, hit up my Disqus below.

