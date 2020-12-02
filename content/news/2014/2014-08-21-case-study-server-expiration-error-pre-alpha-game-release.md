---
id: 9756
title: "Case Study: Server Expiration Error for Pre-Alpha Game Release"
date: 2014-08-21
tags: [ "Case Study"]
---
<img loading="lazy" class="alignright size-full wp-image-9759" style="margin-left: 15px;" src="/assets/img/news/game-post.jpg" alt="game-post" width="160" height="160" data-id="9759" srcset="/assets/game-post.jpg 160w, /assets/game-post-150x150.jpg 150w" sizes="(max-width: 160px) 100vw, 160px" />Today we've got a pretty cool case study that comes to us from a game development studio!

We love to see Exceptionless being used by companies with interesting projects and development pipelines, and what's more interesting than gaming, multi-server, and multi-player environments?

These guys also gave us some good feedback, which we'll address.

Check it out!<!--more-->

## Project

This user is working on a pre-alpha game that is, at the time of the feedback, only available to the in-house team. The game environment requires multiple servers that are deployed via script. When an old version of a server comes down and a new one is deployed, there is cleanup that must happen, etc.

> "I like your product! I've previously written an exception-reporting system that did the same type of thing as Exceptionless but used a mail-server as the exception repository. Since that system was something I had to leave behind at my last company, I wanted to find a solution for my current company, and after comparing alternatives liked what your team had built, so that's what we're using now."

## How Exceptionless Helped

Because the game had such limited players, servers, and testing, it's tough to catch all the little bugs. Fortunately, Exceptionless was able to catch a potentially huge bug that would cause old versions of the servers that were still running to crash because of files being deleted by the new server development clean up scripts.

> "If an old version was still running it would crash because its data-files got deleted. Since we're still in development mode there aren't enough people playing on our game servers to notice this exception &#8212; but we would have when going into alpha or beta test! Fortunately Exceptionless did notice and report this problem."

We think that's pretty awesome, and not just because we're huge nerds!

## Feature Requests & Thoughts

We were lucky enough to get some great feedback from these guys, as well.

### Bug Ownership

> <span style="color: #282f33;">"We'd like a feature that allows our developers to claim ownership of bugs so that they're not seen by others in the Dashboard view by default."</span>

With multiple developers on multiple projects, bugs can stack up and things can get messy. John doesn't need to see Billy's bugs from project A when he's working on his own bugs for project B.

We definitely agree here and understand, but <span style="color: #282f33;">there is a fine line between us being an error reporting service and getting into <a href="/bug-tracking/">bug tracking</a> type features. We had a previous product that tried to do too much and turned people off so we really wanted to try and keep Exceptionless simple. That being said, **we want to make Exceptionless integrate with other apps** much more in the future and make it really easy to create new integrations. We're working on this now with <a title="Upcoming Exceptionless Version 2.0 Overview & Review" href="/upcoming-exceptionless-version-2-0-overview-review/">Exceptionless 2.0, coming soon</a>!</span>

### Multiple Services on Single Server

> "<span style="color: #282f33;">One other thing that was painful for me personally: we run multiple services of the same type on a single server (e.g. multiple instances of "game-server.exe"). In order to ensure that each server has its own queue folder and logfile, I had to write a chunk of custom code."</span>

Again, we totally agree! <span style="color: #282f33;">The <a title="Exceptionless 2.0 Client Rewrite Sneak Peek Usage Example" href="/exceptionless-2-0-client-rewrite-sneak-peek-usage-example/">client in Exceptionless 2.0</a> will be MUCH simpler and will make things much easier. You will be able to easily use in-memory storage and be able to plug in different storage implementations.</span>

## We Love Feedback!

If you're a current user, we'd love to hear how you've used Exceptionless to cut down on bugs and build better apps. If you've got any criticisms or feature feedback/requests, keep those coming as well - they help us improve!

Have an awesome day!


