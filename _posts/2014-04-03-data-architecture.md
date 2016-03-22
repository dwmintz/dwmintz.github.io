---
layout: post
title: "The Building Blocks Of Upworthy's Data Systems"
date: 2014-04-07
comments: false
categories: architecture, analytics
---

_Cross-posted at [Upworthy's R&D Blog](http://upworthy.github.io/2014/04/data-architecture/)_

At Upworthy, we strive to make data-driven decisions whenever possible. So when we started to get serious about capturing and storing our own data, we set out some attributes that our ideal system would have. We wanted our warehouse to be:

- **Understandable** so that anyone in the company — not just analysts — could query it.
- **Scalable** so that it could handle clickstream data for tens or hundreds of millions of monthly visits.
- **Flexible** so that power users (like analysts) could explore the data in ad hoc ways.

Oh, and it couldn't cost a fortune. And since we were starting with only one full-time engineer on the project, it needed to be something that was pretty low-maintenance to maintain.

We figured we wouldn't meet all of these criteria, but they set a good goal to shoot for.

As a first step, we wanted Upworthy's staff to be able to answer ad-hoc questions about our basic object data. But when we initially built and launched Upworthy.com in March 2012, we'd decided to back it with a Mongo database. MongoDB is resolutely non-relational — meaning that it doesn't allow JOINs across collections (Mongo's version of tables).

So even a relatively simple question like "How many posts about gender diversity did our freelancers curate in April?" isn't easily answerable, because it would require joining post data with topic data with curator data. The flexibility that MongoDB gave us in evolving our content management system was great, but for those of us on the analytics side trying to respond to data-hungry colleagues, it quickly became a hindrance.

One option was to migrate our site to a traditional RDBMS. But the prospect of rejiggering our whole site just for analytics seemed impractical. Luckily, before we headed down that path, we heard that the nice folks at Stripe had just open-sourced a new tool called <a href="https://github.com/stripe/mosql" target="_blank">MoSQL</a>. It tails MongoDB's log of operations, and keeps a PostgreSQL slave in sync with the MongoDB master.

To be honest, it sounded both too good to be true, and kind of crazy. But we didn't have anything to lose, and it was really simple to set up — you just map your Mongo collections to tables in PostgreSQL using a simple YAML file, like this.

```
    accounts:
        :columns:
            - _id: TEXT
            - created_at: TIMESTAMP
            - first_name: TEXT
            - last_name: TEXT
```

So we gave it a try and ... it worked. Not only did it work, but it has continued working, stably and reliably, for almost a year now. So that solved our first problem: Our object data was now in an RDBMS.

But our object data is a relatively small dataset — and we were skeptical about whether a traditional RDBMS could manage the larger volume of data we knew we ultimately would want to process. Because really, we knew we'd want to ask questions about events, not just objects. Questions like, "How many Attention Minutes did posts about economics garner in April?" And this would require a more complicated system.

So we started adding Javascript trackers to observe all the client-side events we cared about, and report them to our servers. The problem was, once we had the events recorded, we needed somewhere to put them. And while our PostgreSQL database could handle data for a few thousand posts and a few dozen curators, it wasn't going to gracefully handle querying tens of millions of daily events without some serious tuning. Even then, many of the queries we'd want to run would be pushing the limits of what PostgreSQL could do without having to wait hours or days for results.

A few of our engineers had experience using Vertica, a popular data warehousing solution. But particularly with only one dedicated engineer and a limited budget, that seemed like overkill for what we needed. Luckily, AWS had just introduced their columnar data warehousing solution, <a href="http://aws.amazon.com/redshift/" target="_blank">Redshift</a>, and several friends suggested we give it a shot.

So we spun up a small cluster (yay for paying by the hour!) and tried it out. And we were very impressed.

From the analysts' perspective, Redshift was just a slightly modified version of PostgreSQL. Except it was blazingly fast, even when running complex queries with several Common Table Expressions and a bunch of JOINs on many millions of rows. And from the engineers' perspective, Redshift was great because maintenance was handled by AWS, it was easily scalable WAY beyond where we're at now, and reserved instances brought our cost per TB down to about $2,000/year.

So at that point, we had a data warehouse that could easily handle all our data, didn't cost a fortune, required very little maintenance, and could tolerate as much ad hoc querying as the analysts' hearts desired. Not too shabby.

The only thing left on our wish list was a way for people who don't speak SQL to explore the data.

Enter <a href="http://looker.com/" target="_blank">Looker</a>.

One of our investors had mentioned Looker, a business intelligence startup, and when we talked to their team, we were really impressed. They didn't tell us our schema had to fit their one-size-fits-all specifications, and they were happy to let us explore all of our data without charging us extra. In fact, they set up an instance for us in just a few minutes  and let us start querying our data immediately.

Because Looker's data explorer is a point-and-click web application, the rest of our team can use it as easily as the analysts — no SQL experience required. And because it exposes the SQL it's running on our data warehouse, our analysts quickly figured out how to get the most out of the tool.

So, to our surprise, we had a system that met all of our goals. And all thanks to a bunch of tools that were less than a year old. But there's one more thing.... (sorry, couldn't resist).

This gave us a data warehouse that had a 24-hour ETL cycle. That was pretty good, but we were eager to find ways to get that ETL cycle shorter. We had looked at powerful stream processors like Flume and Kafka. But again, small team, limited resources.

At the end of 2013, almost as if they'd been listening to our internal deliberations, AWS rolled out <a href="http://aws.amazon.com/kinesis/" target="_blank">Kinesis</a>. Kinesis provided the stream processing functionality we needed, without the dev/ops overhead that comes with standing up your own stream processor. (AWS's slogan really should be, "We give you all the functionality of *[cool thing x]* without the hassle of having to build *[cool thing x]* yourself.")

This week, after a few months' work by our now-2.5-person analytics engineering team, we're rolling out our "fast data pipeline." Instead of up to 24 hours of latency, our new pipeline is more like 3-5 minutes behind. So yeah: MoSQL, Redshift, Looker, Kinesis. Give 'em a look. And give us a shout if you have questions.

(For the record, these are the folks who actually build this stuff: [Zane Shelby](https://twitter.com/zaneshelby), [Anders Conbere](https://twitter.com/aconbere), and [Pavel Repin](https://twitter.com/pavelrepin).)
