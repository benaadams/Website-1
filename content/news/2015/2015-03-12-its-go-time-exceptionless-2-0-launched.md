---
id: 12749
title: IT'S GO TIME - Exceptionless 2.0 Launched!
date: 2015-03-12
---
![version-2.0-launched](/assets/img/news/version-2.0-launched.png)Today, after much development and [weeks of live user testing and feedback](#preview), we have officially released Exceptionless 2.0 into the wild!

Users will notice a completely new interface and experience **numerous new features and improvements**, highlighted below. Existing users that <a title="Update Exceptionless Client to 2.0" href="/docs/self-hosting/upgrading-self-hosted-instance/" target="_blank">update their clients</a> (not required) will experience improved client efficiency, the ability to send us logs, and more. We believe 2.0 will usher in a new era in event reporting and logging, becoming a true asset to developers everywhere.

Shipping 2.0 out to our amazing customers has us **overwhelmed with excitement**, and we can't wait to see all the new ways in which Exceptionless will be used to squash bugs and improve apps everywhere. Read on for more details on updating existing clients and all the new features and changes. **We know you'll love it.**

<div class="signup center">
  <a class="btn btn-large btn-primary" href="https://be.exceptionless.io/" target="_blank">Check Out Exceptionless 2.0 Now!</a>
</div>

<!--more-->

## Updating Clients for Existing Users

Follow these quick and easy steps below to update your Exceptionless client to 2.0.

  1. Open the NuGet Package Manager dialog.
  2. Click on the Updates tab.
  3. Select the Exceptionless NuGet packages and click the Update button.
  4. **You should be good to go!
** If you need more info, view our <a title="Upgrading Exceptionless" href="/docs/self-hosting/upgrading-self-hosted-instance/" target="_blank">updating documentation</a> or contact us via in-app support. We're always here to help if you have any questions!

## Exceptionless 2.0 Feature Recap

### Check out these awesome new and improved features<figure id="attachment_12762" class="thumbnail wp-caption alignright" style="width: 150px">

![Exceptionless 2.0 Screenshot](/assets/img/news/version-2-launch-screenshot-150x150.jpg)

Exceptionless 2.0 is faster, sleeker, mobile-friendly, more functional, includes all the below major improvements, and has countless smaller tweaks and changes we poured our heart and soul into. It's a whole new system - check it out!

* **Searching / Filtering**
    We’ve implemented Elasticsearch and you can search/filter ALL the things! Read more <a title="Exceptionless 2.0 Elasticsearch" href="/making-move-elastic-search-exceptionless-2-0/" target="_blank">here</a> and watch a quick demo video <a title="Exceptionless Search Filters" href="/filter-your-exceptions-video-demo/" target="_blank">here</a>.

* **Cross Organization Views**
    You now have the ability to view all events across all organizations, a single organization, or a project.

* **PCL Support**
    We’ve built in client support for <a title="Exceptionless.Portable" href="https://www.nuget.org/packages/exceptionless.portable" target="_blank">portable class libraries</a>!

* ****New Clients!
**** Including: <a title="Exceptionless.Portable" href="https://www.nuget.org/packages/exceptionless.portable" target="_blank">Exceptionless.Portable</a> for console apps and <a title="Exceptionless NLOG Client" href="http://www.nuget.org/packages/exceptionless.nlog" target="_blank">Exceptionless.NLog</a>, an nlog target that reports to Exceptionless

* **Fully Documented API**
    For all your API needs, check out the <a title="Exceptionless API Documentation" href="https://api.exceptionless.io/docs/index.html" target="_blank">API Documentation</a>

* **Bulk Actions
** Select multiple events or instances of events and do with them as you please! <a title="Exceptionless 2.0 Bulk Actions" href="/news/2014/2014-12-12-bulk-actions-sneak-peak-exceptionless-2-0-video" target="_blank">Watch the preview demo.</a>

* **Faster than Ever!
** Exceptionless 2.0 is a single page app (SPA) and is lightning fast. <a title="Exceptionless 2.0 AngularJS" href="/news/2014/2014-10-23-angularjs-exceptionless-2-0" target="_blank">We’re using AngularJS</a> and we’re stoked to give our users a super quick experience!

<li id="preview">
  **And more…<br /> **Check out more new features, including source links, in our <a title="Exceptionless 2.0 Overview" href="/news/2014/2014-08-13-upcoming-exceptionless-version-2-0-overview-review" target="_blank">Exceptionless 2.0 Overview article</a>. Includes details on: Event Based Reporting System, Simplified API, The Pluggable System, Client Rewrite, New Message Bus & Queuing, and Job System Enhancement.
</li>

## Live User Testing Review & Notes

**Our live preview went great! Thank you EVERYONE that sent feedback and comments.**

We received some awesome feedback from many of our customers, made some UI/usability tweaks and improvements, and fixed a few minor bugs. We also added the ability to search custom fields, which is a pretty big deal for some.

Naturally, we used Exceptionless 2.0 to log, report on, and gather data for the preview - and it worked amazingly! (shameless, but true, promotion)

On average, we traced **200,000+ anonymous log messages** within the app **each day** from preview activity. That data allowed us to learn a lot more about the behavior of Exceptionless 2.0 in areas such as jobs and gave us additional insight into what was going on. We were able to use a combination of errors, logs, and feature usage metrics to track down and fix an issue with external logins, as well. Awesome!

The system also helped us track down and identify a performance issue that we were able to fix and improve.

Overall, we had no major surprises and were able to tweak and improve several pieces of the app that we think will make it even more awesome.

## Keep The Feedback Coming

No software application is ever "done," so make sure to keep the feedback coming. We've made a huge leap from Exceptionless 1.x, but we want to keep improving the system in all areas. **We love hearing from our users**, and respond to each email, in-app message, website form submission, etc. So, please, let us know what you think!
