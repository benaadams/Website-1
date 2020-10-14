---
id: 13235
title: JavaScript Client Demo &#8211; Exceptionless
date: 2015-05-27
---
<img loading="lazy" class="aligncenter size-full wp-image-13237" src="/_site/assets/blog-header-javascript.jpg" alt="Exceptionless JavaScript Client" width="708" height="250" data-id="13237" srcset="/assets/blog-header-javascript.jpg 708w, /assets/blog-header-javascript-300x106.jpg 300w" sizes="(max-width: 708px) 100vw, 708px" />

We're getting closer and closer to version 1.0 of our <a title="Exceptionless JavaScript Client" href="/javascript-client-available-for-preview-testing/" target="_blank">JavaScript client</a>, and we wanted to give everyone a demo of installation, configuration, and usage.

If you're using Node.js, make sure to check out last week's blog post for <a title="Exceptionless Node.js Demo" href="/exceptionless-node-js-javascript-client-demo/" target="_blank">Node specific examples</a>. Otherwise, continue reading for Javascript examples.

As you read and begin playing with the Exceptionless JavaScript client, please make note of any feedback, bugs, etc, and <a title="Exceptionless.JavaScript GitHub Repo" href="https://github.com/exceptionless/Exceptionless.javascript/issues" target="_blank">submit a GitHub issue</a> so we can fast track version 1.0 &#8211; we surely appreciate it!

<!--more-->

## How the JavaScript Client was Built

We built our JavaScript client in <a title="TypeScript" href="https://github.com/Microsoft/TypeScript" target="_blank">typescript 1.5</a> transpiled it to es5. Our single client works with both <a title="Exceptionless.JavaScript Node.js Demo" href="/exceptionless-node-js-javascript-client-demo/" target="_blank">Node.js</a> and JavaScript due to dependency injection and a <a title="Universal Module Definition (UMD)" href="https://github.com/umdjs/umd" target="_blank">Universal Module Definition (UMD)</a>.

## Installing the Exceptionless JavaScript Client

### Via Bower

  1. Install the package by running `bower install exceptionless`
  2. Add the Exceptionless script to your HTML page. We recommend placing the script at the top of the document to ensure Exceptionless picks up and reports the absolute most potential exceptions and events.

<pre class="brush: xml; title: ; notranslate" title="">&lt;script src="bower_components/exceptionless/dist/exceptionless.min.js"&gt;&lt;/script&gt;</pre>

## Configuring the Client

Configuration of the Exceptionless JavaScript client can be accomplished a variety of ways. We list the common ways below, but make sure to check the <a title="Exceptionless Javascript Client GitHub Page" href="https://github.com/exceptionless/Exceptionless.JavaScript" target="_blank">Exceptionless.JavaScript GitHub repo</a> for the most up to date documentation if you run into any problems using this example code.
_NOTE: The only required setting you need to configure is the client's apiKey._

### Configuration Options

**1.** Configure the `apiKey` as part of the script tag. This method will be applied to all new instances of the ExceptionlessClient

<pre class="brush: xml; title: ; notranslate" title="">&lt;script src="bower_components/exceptionless/dist/exceptionless.min.js?apiKey=API_KEY_HERE"&gt;&lt;/script&gt;</pre>

**2.** Set the `apiKey` on the default ExceptionlessClient instance.

<pre class="brush: jscript; title: ; notranslate" title="">var client = exceptionless.ExceptionlessClient.default;
client.config.apiKey = 'API_KEY_HERE';</pre>

**3.** Create a new instance of the ExceptionlessClient and specify the `apiKey` or <a title="Exceptionless.JavaScript Configuration Object" href="https://github.com/exceptionless/Exceptionless.JavaScript/blob/master/src/configuration/IConfigurationSettings.ts" target="_blank">configuration object</a>. _Note that the configuration object is optional._

<pre class="brush: jscript; title: ; notranslate" title="">var client = new exceptionless.ExceptionlessClient('API_KEY_HERE'); // Required

// or with a configuration object
//var client = new exceptionless.ExceptionlessClient({
  //apiKey: 'API_KEY_HERE',
  //submissionBatchSize: 100
//});</pre>

## Sending Events

Unhandled exceptions will automatically be sent to your Exceptionless dashboard once the JavaScript client is configured properly. In order to send additional events, including log messages, feature usages, and more, you can use the code samples below and check the <a title="Exceptionless.JavaScript GitHub Repo" href="https://github.com/exceptionless/Exceptionless.JavaScript" target="_blank">Exceptionless.JavaScript GitHub Repo</a> for the latest examples and documentation.

### Sending Log Messages, Feature Usages, etc

<pre class="brush: jscript; title: ; notranslate" title="">var client = exceptionless.ExceptionlessClient.default;

client.submitLog('Logging made easy');

// You can also specify the log source and log level.
// We recommend specifying one of the following log levels: Trace, Debug, Info, Warn, Error
client.submitLog('app.logger', 'This is so easy', 'Info');
client.createLog('app.logger', 'This is so easy', 'Info').addTags('Exceptionless').submit();

// Submit feature usages
client.submitFeatureUsage('MyFeature');
client.createFeatureUsage('MyFeature').addTags('Exceptionless').submit();

// Submit a 404
client.submitNotFound('/somepage');
client.createNotFound('/somepage').addTags('Exceptionless').submit();

// Submit a custom event type
client.submitEvent({ message = 'Low Fuel', type = 'racecar', source = 'Fuel System' });</pre>

### Manually Sending Errors

To manually send events other than the automatically reported unhandled exceptions, you can use our fluent <a title="Exceptionless.JavaScript Event Builder API" href="https://github.com/exceptionless/Exceptionless.JavaScript/blob/master/src/EventBuilder.ts" target="_blank">event builder API</a>.

The below example demonstrates sending a new error, &#8220;test,&#8221; and setting the ReferenceID, Order and Quote properties, Tags, Geo, UserIdentity, and marking it as Critical.

<pre class="brush: jscript; title: ; notranslate" title="">var client = exceptionless.ExceptionlessClient.default;

try {
  throw new Error('test');
} catch (error) {
  client.createException(error)
    // Set the reference id of the event so we can search for it later (reference:id).
    // This will automatically be populated if you call client.config.useReferenceIds();
    .setReferenceId('random guid')
    // Add the order object (the ability to exclude specific fields will be coming in a future version).
    .setProperty("Order", order)
    // Set the quote number.
    .setProperty("Quote", 123)
    // Add an order tag.
    .addTags("Order")
    // Mark critical.
    .markAsCritical()
    // Set the coordinates of the end user.
    .setGeo(43.595089, -88.444602)
    // Set the user id that is in our system and provide a friendly name.
    .setUserIdentity(user.Id, user.FullName)
    // Submit the event.
    .submit();
}</pre>

## What Data is Collected?

We built the JavaScript client to be full featured and allow you to report and log all the data our other clients do. It has a fluent API, as mentioned above, and is ready to rock and roll.

We wire up to the window.onerror handler by default, in order to send unhandled exceptions to your Exceptionless dashboard automatically.

Finishing off the Exceptionless JavaScript client features, every event also includes request information.

A few screenshots of an individual event can be found below.<figure id="attachment_13248" class="thumbnail wp-caption alignleft" style="width: 150px">

[<img loading="lazy" class="wp-image-13248 size-thumbnail" src="/assets/javascript-client-event-overview-150x150.png" alt="Exceptionless Javascript Event Overview" width="150" height="150" data-id="13200" />](/_site/assets/javascript-client-event-overview.png)<figcaption class="caption wp-caption-text">Event Overview</figcaption></figure> <figure id="attachment_13249" class="thumbnail wp-caption alignleft" style="width: 150px">[<img loading="lazy" class="wp-image-13249 size-thumbnail" src="/assets/javascript-client-exception-details-150x150.png" alt="Exceptionless Javascript Event Details" width="150" height="150" data-id="13201" />](/_site/assets/javascript-client-exception-details.png)<figcaption class="caption wp-caption-text">Event Details</figcaption></figure> <figure id="attachment_13250" class="thumbnail wp-caption alignleft" style="width: 150px">[<img loading="lazy" class="wp-image-13250 size-thumbnail" src="/assets/javascript-client-event-request-info-150x150.png" alt="Exceptionless Javascript Event Request Details" width="150" height="150" data-id="13202" />](/_site/assets/javascript-client-event-request-info.png)<figcaption class="caption wp-caption-text">Request Details</figcaption></figure>

<h2 style="clear: both;">
  Sample
</h2>

We have put together an <a href="https://github.com/exceptionless/Exceptionless.JavaScript/tree/master/example" target="_blank">example</a> that you can use to get an idea of how everything works. It is available on the <a href="https://github.com/exceptionless/Exceptionless.JavaScript/tree/master/example" target="_blank">GitHub Repo</a>.

### To Get the Example Running&#8230;

  1. Clone or download the <a href="https://github.com/exceptionless/Exceptionless.JavaScript/tree/master/example" target="_blank">GitHub Repo</a>
  2. Edit the HTML file in the root example folder and replace the <a href="https://github.com/exceptionless/Exceptionless.JavaScript/blob/master/example/index.html#L8" target="_blank">existing API Key</a> with yours. Also, comment out the <a href="https://github.com/exceptionless/Exceptionless.JavaScript/blob/master/example/index.html#L16" target="_blank">serverUrl</a>.
  3. Open the HTML file in your browser
  4. Open the console so that you can see the debug messages that the example generates
  5. Click the buttons on the page to submit an event

<h2 style="clear: both;">
  Troubleshooting
</h2>

Calling `client.config.useDebugLogger();` to enable debug logging is recommend and will output messages to the console regarding what the client is doing. Please <a title="Exceptionless JavaScript Client Issues" href="https://github.com/exceptionless/Exceptionless.javascript/issues" target="_blank">contact us by creating an issue on GitHub</a> if you need help or have any feedback regarding the JavaScript client.

## Feedback

As we move forward towards version 1.0 of our JavaScript client, we are looking for any and all feedback, so please don't hesitate to <a title="Exceptionless JavaScript Client Feedback" href="https://github.com/exceptionless/Exceptionless.javascript/issues" target="_blank">let us know what you think, report a bug, etc</a>.

Happy coding!