+++
author = "Steven Herod"
categories = ["howto"]
date = 2017-07-27T00:00:00Z
description = ""
draft = false
image = "https://images.unsplash.com/photo-1528642474498-1af0c17fd8c3?ixlib=rb-1.2.1&q=80&fm=jpg&crop=entropy&cs=tinysrgb&w=2000&fit=max&ixid=eyJhcHBfaWQiOjExNzczfQ"
slug = "mass-unfollowing-people-on-linkedin"
summary = "\nI’m a believer in LinkedIn. I find it useful on a personal and professional level and I have viewed it as a useful newsfeed over many…\n"
tags = ["howto"]
title = "Mass Unfollowing People on LinkedIn"

+++


I’m a believer in LinkedIn. I find it useful on a personal and professional level and I have viewed it as a useful newsfeed over many years.

But LinkedIn has a sickness, and I’d summarise it as ‘Facebookitis’.

Over the years posts have pivoted from industry, technology and company news to a variety of ‘inspirational’ stories of various quality. (And I’m not referring to actual ‘inspiration’, rather a collection of self serving homilies, often repeated.)

And that’s fine, if people want to do that, they can. The trouble is, with many many connections and the habit of the LinkedIn feed to push posts others have liked into my feed I’m finding the content less and less valuable.

Sadly, LinkedIn gives you very little ability to thin out the noise and it gives you no way to ‘mass edit’ who you follow.

You are condemned to unfollow each individual one at a time, and that’s not a valid use of anyone’s time.

So here is a quick and slightly nuclear approach to solving the problem and unfollowing everybody (As at July 2017, if LinkedIn changes its styles, this won’t work).

1. Go to this page on your profile: [https://www.linkedin.com/feed/following/](https://www.linkedin.com/feed/following/)
2. Open the Developer Tools in Chrome.
3. Scroll down, several times, whilst LinkedIn lazy loads a decent sized list
4. In the Console View, type:

```
var c = document.querySelectorAll("button.is-following"); for (i in c) { c[i].click() }
```

and press enter;

5. Reload the page, and repeat the process, until the ‘Following’ count drops down and the page says ‘Follow Fresh Perspectives’

6. Re-follow key people

Enjoy your cleaned up feed.

