---
layout: post
title: "What Uniques And Pageviews Leave Out (And Why We're Measuring Attention Minutes Instead)"
date: 2014-02-06
comments: false
categories: analytics, media, metrics
---

_Cross-posted at [Upworthy Insider](http://blog.upworthy.com/post/75795679502/what-uniques-and-pageviews-leave-out-and-why)_

We’re big believers that you are what you measure. Our mission here at Upworthy is to draw massive amounts of attention to the most important topics. So, how do you measure that?

We dabbled with pageviews, but that’s a flimsy metric, as anyone who’s suffered through an online slideshow knows (20 pageviews! Zero user satisfaction!). Pageviews are only a great metric if you’re being paid for each pageview; we don’t run banner ads, so they’ve never meant as much to us.

Unique visitors are fine but reward breadth over depth of user experience. Shares per piece of content are quite a valuable signal, but they don’t get you all the way there. And time on site, as Google measures it, works great for e-commerce but is often confusingly broken for media companies. Google Analytics at one point had us at 21 minutes on site per visit on average; we’re good, but we know we’re not that good.

So we decided we needed a new approach. If we’re trying to maximize attention for meaningful content, let’s actually solve for that.

<!--more-->

Introducing *attention minutes*, Upworthy’s new primary metric, which we’re planning to track in two forms:

* *Total Attention on Site* (per hour, day, week, month, whatever) — that tells us (like total uniques or total pageviews) how good of a job Upworthy is doing overall at drawing attention to important topics.

* And *Total Attention per Piece*, which is a combination of how many people watch something on Upworthy and how much of it they actually watch. Pieces with higher Total Attention should be promoted more.

We love thinking this way because it rewards us for sharing content that people really enjoy and find valuable — not just stuff they click on a lot. It may mean that we don’t do quite as well on uniques or pageviews, but that’s a trade-off we’re happy to make because this is a metric focused on real audience satisfaction.

How does it work? Attention minutes is a fine-grained, conservative measure of how long people are engaging with the content on our pages. [YouTube](https://www.youtube.com/yt/press/statistics.html), [Chartbeat](http://blog.chartbeat.com/2013/03/18/using-engaged-time-to-understand-your-audience/), and [Medium](https://medium.com/data-lab/mediums-metric-that-matters-total-time-reading-86c4970837d5) are all moving in a similar direction: They’ve all recognized the advantages of measuring whether visitors are actually engaged with their content and have rolled out similar measures in recent months.

Our implementation is far more precise than “Time on Page” as it’s usually measured. Time on Page generally relies on a very sparse set of signals to figure out whether viewers are still paying attention. And especially on the last page of a visit, it can be hugely misleading. (Here’s a [handy explainer](http://gatipoftheday.com/average-time-on-page-average-visit-duration-and-browser-timestamps/) about why that is. Incidentally, our Average Time on Page was 5:24 in December and January according to Google Analytics. But we just don’t think that metric is terribly reliable or useful for our purposes.)

We built attention minutes to look at a wide range of signals — everything from video player signals about whether a video is currently playing, to a user’s mouse movements, to which browser tab is currently open — to determine whether the user is still engaged. The result is a fine-grained and unforgiving metric that tells us whether people are really engaged with our content or whether they’ve moved on to the next thing.

In the charts below, we show what attention data for three popular posts looks like from the last couple of months. As you can see, attention follows very different patterns for different posts. The first one looks great if you only look at pageviews. (1 million pageviews! Woohoo!) But when you look more closely, it’s not driving much attention per pageview. The second post had far fewer pageviews but more total attention minutes. And the last post had about the same pageviews as the first but vastly more total attention minutes.

![Pageviews vs. Attention Minutes]({{ site.url }}/images/attmin_examps.png)

Being able to make charts like this helps us get past the focus on pageviews to see what’s really grabbing our visitors. They allow us to focus not just on how many people landed on a page but how many people watched a substantial portion. That’s how we define our biggest successes.

Last quarter, the Upworthy community spent more than 7 million attention minutes on our site per day. That’s more than 13 years of attention, every day. We’re pretty proud of that. But we’ve got a long way to go. (For reference, American adults watch 79,000 years of television per day.)

![Attention Goals]({{ site.url }}/images/attmingoals.png)

We also think this is how social networks will want to think about the content being shared on their sites — not just in terms of clicks or shares but in terms of what’s grabbing users’ attention. A comprehensive approach that looks at clicks + watchability (attention minutes) + shares + engagement (comments and Likes) can give a strong signal about which content users find highly satisfying and rewarding, and which content they’re bored by.

In the coming months, we’ll be making the details of our implementation, including the source code, public; we’re excited to have other media companies engage with this metric. We think adding attention minutes to the arsenal of metrics that publishers look at will accelerate the drive toward quality. The media landscape is constantly changing, and how we judge success needs to evolve constantly, too. We think attention minutes is a step in a better direction.
