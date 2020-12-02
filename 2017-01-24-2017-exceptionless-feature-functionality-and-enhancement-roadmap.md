---
id: 15220
postTitle: 2017 Exceptionless Feature, Functionality, and Enhancement Roadmap
date: 2017-01-24T10:14:45-06:00
author: Exceptionless
layout: blog_post.liquid
tags: ["posts", ".NET"]
---
<img loading="lazy" class="aligncenter size-large wp-image-15226" src="/assets/elasticsearch-2017-roadmap-header-1024x538.jpg" alt="exceptionless feature roadmap for 2017" width="940" height="494" data-id="15226" srcset="/assets/elasticsearch-2017-roadmap-header-1024x538.jpg 1024w, /assets/elasticsearch-2017-roadmap-header-300x158.jpg 300w, /assets/elasticsearch-2017-roadmap-header-768x403.jpg 768w, /assets/elasticsearch-2017-roadmap-header.jpg 1200w" sizes="(max-width: 940px) 100vw, 940px" />

Can you believe it's almost February already! Us either. No rest for the whicked, though, as we sit down to get cranking on our list of Exceptionless changes for 2017.

We have a a great list of features, functionality changes, and enhancements planned, and no doubt we'll work in a few other popular feature requests and, naturally, bug fixes along the way.

Let's take a look at the primary roadmap, shall we?<!--more-->

## Upgrading to Elasticsearch 5

Upgrading to Elasticsearch 5 has been in the works for some time now, with early testing starting in late 2016. As of January 23rd, we have <a href="https://github.com/exceptionless/Exceptionless/issues/145" target="_blank">officially pushed the upgrade to production</a> and are looking for feedback, missed bugs, and performance improvement reports from anyone using it!

### Primary Elasticsearch 5 Benefits

* Elasticsearch 5 is the latest version of [ElasticSearch](https://www.elastic.co/products) and brings in massive improvements to event indexing speed, reduced memory sizes, and much more.
* The Elasticsearch libraries support .NET Core, bringing us one step closer to fulfilling a vision that includes cross-platform support.
* Our new implementation is built on a new, faster Microsoft Azure and SSD storage infrastructure. This will greatly increase the indexing and searching performance,  reducing dashboard latencies, among other things.
* With the power of <a href="https://github.com/exceptionless/Foundatio.Parsers" target="_blank">Foundatio.Parsers</a> project, we have gained the ability to consume generic aggregations and pivot/report on data any way our users like it.
* This upgrade also makes it easier to self host through the use of containers. Our goal is to move the entire app to use containers, which will allow you to self host in seconds!
* We will now be doing daily indexes for more performance, fine grained backups, and the ability to more quickly change our indexes.

## Future Exceptionless Notification Changes

We're always working on notifications, we've got <a href="https://github.com/exceptionless/Exceptionless/issues/177" target="_blank">several distinct changes we want to work on in 2017</a>. Here are a few of the important ones:

* We will continue working on rich, rule based notifications for email, services like Slack and Hipchat, and more.
* Pausing notifications will soon be a thing!
* You'll also be able to set up notifications based on the rate of events, so you can know when issues are ramping up or getting out of hand.
* Lastly, you will be able to receive a periodic digest email based on activity.

## Porting to .NET Core and Containers

* We want to port the Exceptionless app to [.NET Core](https://www.microsoft.com/net/core) so we can run it anywhere (macOS, Linux or Windows).
* Running on .NET Core also brings massive performance improvements and lower overhead, which will have positive trickle down affects throughout the app.
* Once we support .NET Core, we can containerize the entire app, allowing us to scale more easily.
* These changes will make self hosting super simple. You'll basically be able to run &#8220;docker run -d exceptionless\`&#8221; and be done!

## Custom Exceptionless Dashboards

We know the dashboard is crucial for many things, and we want to make them more customizable to fit each user's individual cases. At the same time, we want to make sure we maximize business value. So, we plan on working on several <a href="https://github.com/exceptionless/Exceptionless/issues/229" target="_blank">features and functional aspects of dashboards</a>, namely:

* Creating pre-define dashboards that are more granular, such as device usage, breakdown by exception type, etc.
* Allow users to create their own custom dashboards.

## New Exceptionless Clients

We really want to add new native clients to Exceptionless, and are including that as a major goal for 2017. Everything we are working on is moving in that direction, one way or the other, and we hope to make further announcements in this department soon!

We are, of course, always accepting pull requests as well!

## What Are We Missing?

What have we forgotten? We know everything isn't included on this list, but if we have missed something big that you can't live without, please let us know!

Otherwise, look for a new version announcement **very soon**, and get ready to upgrade and take advantage of several of these new upcoming changes.
