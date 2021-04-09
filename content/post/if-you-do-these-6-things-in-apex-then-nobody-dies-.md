+++
author = "Steven Herod"
date = 2016-05-29T00:00:00Z
description = ""
draft = false
image = "https://images.unsplash.com/photo-1549816044-47649bae10f6?ixlib=rb-1.2.1&q=80&fm=jpg&crop=entropy&cs=tinysrgb&w=2000&fit=max&ixid=eyJhcHBfaWQiOjExNzczfQ"
slug = "if-you-do-these-6-things-in-apex-then-nobody-dies-"
title = "If you do these 6 things in Apex then nobody dies."

+++


There is a lot of advice in programmer land, advice that often mixes mandatory practices with suggestions that are ‘good to do’.

Translated outside of programming, these lists often look like:

1. Call your mother.Obviously good advice and all of us who can should do that, but if you don’t you aren’t going to die (Although you may want to if she calls).
2. Don’t eat saturated fatsAlso good advice, but the affect is not immediately obvious and its only over many years you may find it a problem
3. Do not attempt to cut your toe nails with a chainsaw.Very clearly a bad idea and on a different level of wrong.

For a novice the list above can be difficult to parse and figuring out the nice to haves from the ‘this will kill you’ isn’t obvious

So I’ve decided to make it easier by providing 1 simple list of all the things that when developing with apex WILL KILL YOU.

### Do not put SOQL in loops.

Not ever, no. Don’t. There is no excuse, it WILL cause your code to crash, it will turn up in code reviews (automated). People will find it and curse your name. Don’t do it. Ever.

### Do not put DML in loops

Same as above. It will fail, it is slower and it helps no one.

### You must use asserts in tests.

No asserts, you didn’t write a test. No excuse, you’re just wasting your time and everybody else’s.

### Do not use (SeeAllData=true) unless Salesforce makes you.

Using existing data in an org is madness. It won’t work in a Sandbox, it won’t work if things change. The ‘making you’ modifier is related to the dark corners of Salesforce like the Chatter API which requires you to use it. Best case — don’t use the Chatter API in Apex.

### Use one trigger per object.

A few years ago I didn’t really get this rule, then I spent too much time in orgs with multiple triggers on single objects. It makes things unpredictable and unpredictable code is bad code. Bad code will hurt you.

### Do not cut and paste code you don’t understand.

If your train of thought is ‘I think this does what I want, so I’m just going to copy it’ then you’ve done the programming equivalent of closing your eyes and walking into traffic. You should have your Ctrl/Cmd key removed. Stop it.

### The final word…

Lets be clear, if you knowingly do any of the things in this list and think ‘oh, it’ll be okay’ or worse ‘I don’t care’ then I think you are incompetent and you should find another job.

Harsh? Yes. But you’re being paid to do this, show some goddamn pride.

Memorize this list, print it out and do not forget.

{{< figure src="/images/downloaded_images/If-you-do-these-6-things-in-Apex-then-nobody-dies-/0-96zlrJYECrPWXUUu.jpg" >}}

