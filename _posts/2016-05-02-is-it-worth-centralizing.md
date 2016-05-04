---
layout: post
title: "Is It Worth Centralizing My Data?"
date: 2016-05-02
comments: false
categories: architecture, data warehousing
---

At Looker, we talk to a lot of companies about their data. One of the most common conversations we have is around centralizing data. We’re big advocates of getting all the data you care about in one place, and, because that’s not a trivial process, we often get questions about how valuable centralization really is.

So I wanted to walk through the three huge advantages I’ve seen centralized data give companies. *Fundamentally, it comes down to convenience, consistency, and connections.*

<!--more-->

The first is the simplest: _*Having all your data in one place is way more convenient than having it dispersed across many platforms.*_

It’s easy to write off the cost of having to separately log into Google Analytics for web traffic stats, Salesforce for account data, your CMS for content tags, Facebook for social data, and your email service provider for open rates. But when you multiply all the employees who are doing this by the minutes (or hours) they spend each time they have to recombine those data sources in Excel, it adds up. You might think of it as wasted minutes, but across the company, it’s actually whole days and weeks that are going down the drain.

_*The second reason to centralize your data is consistency.*_ At Looker we refer to the problem posed by inconsistent data as “data chaos” and we see lots of companies that suffer from it. Each department has access to the data it cares about, but imposes its own meaning on the data because there’s no coordination. Worse, that meaning resides on individuals’ computers in horribly complicated Excel “programming.”

That’s problematic for lots of reasons (the first of which you’re probably familiar with if you’ve ever tried to debug an Excel formula gone bad). But the one that can actually sink your business is that when your business logic lives in tens or hundreds of places, there’s no guarantee that everyone is living by the same definitions.

In fact, I’d bet dollars to donuts that they’re not using the same definitions. And so that means when everyone gets in the quarterly review, and Finance’s definition of an active customer is different than Support’s, both of which are different from Marketing’s, things can get ugly.

By centralizing your data, and unifying the business logic that gives your data meaning in a data platform like Looker, you ensure that everyone in the company is using the exact same definition of Average Order Value, and that if you change that definition, it updates for everyone. (For a rundown on how valuable this process can be for creating a data-driven culture, check out [this great post by Carl Anderson](http://www.p-value.info/2015/04/creating-data-driven-organization-two_6.html), Warby Parker’s Director of Data Science.)

The last reason to centralize your data is the most intangible, but also by far the most valuable. *_Until you have your data in one place, the hassle of joining one system’s data to another’s is so costly that you’re almost certainly missing out on critical insights that live in the data._*

I can’t know ahead of time which of these connections will fundamentally change your business, but I also can’t tell you how many times I’ve seen it happen. Whether it’s finally being able to see how different the lead-to-win funnel looks when it’s grouped by lead source, or that [refund requests spiked after a change to your product’s interface](http://blog.venmo.com/hf2t3h4x98p5e13z82pl8j66ngcmry/2014/8/27/data-driven-design), or that Account Execs who communicate with prospects more frequently during trials close deals at higher rates, you’ll only truly unlock your data’s power to change your business when you can make connections across all of the data.

So, when you’re trying to decide whether it’s worth the work it’ll take to get all your data centralized--whether the reason is convenience, consistency, or the new connections you’ll be able to see--the answer is yeah, it’s worth it.
