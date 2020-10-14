---
id: 13900
title: Using Reference Ids for Better Customer Service
date: 2015-12-17
---
<img loading="lazy" class="aligncenter size-full wp-image-13908" style="margin-bottom: 20px;" src="/assets/reference-ids-blog-header-image.png" alt="Exceptionless Reference IDs" width="708" height="250" data-id="13908" srcset="/assets/reference-ids-blog-header-image.png 708w, /assets/reference-ids-blog-header-image-300x106.png 300w" sizes="(max-width: 708px) 100vw, 708px" />

This week we want to talk about **reference Ids** and how we use them to **improve customer service** for Exceptionless. And how we think you can do the same for your users.

## What's a Reference Id?

A reference id is a unique identifier, generated by the user, that allows you to look up a submitted event at a later time. This is important because _event Ids are not created until after the event is processed_, so there is no other way to look up an event. We also use Reference Ids to help deduplicate events server side, which is another reason why it’s important that they are unique.

## Using Reference Ids for the Greater Good

<!--more-->

One of the ways we use Reference Ids is to **support end users**, something that is very important to us. There is nothing more frustrating than being unable to help a user that is experiencing a problem because you don’t know what they are seeing (when there could be thousands of errors in your app).

To combat this issue, we always try to include a reference Id with every error message shown to the user. This allows end users to contact us with a Reference Id and receive help **immediately** for the error they are seeing because we can **easily track down and view it**.

## Reference Id Example

The Exceptionless clients have built in support to generate and track unique Reference Ids for every error event. Behind the scenes, we register a default Reference Id plugin that sets a Reference Id on submitted error events and stores the Reference Id in an implementation of <a>ILastReferenceIdManager</a>. The Reference Id manager’s goal is just to persist and retrieve the last used Reference Id.

Since this is a default plugin, we can enable this behavior by calling the `UseReferenceIds()` method on the configuration object to register the default Reference Id on every error event.

### C# Example

<pre class="brush: csharp; title: ; notranslate" title="">using Exceptionless;
ExceptionlessClient.Default.Configuration.UseReferenceIds();</pre>

### JavaScript Example

<pre class="brush: jscript; title: ; notranslate" title="">exceptionless.ExceptionlessClient.default.config.useReferenceIds();</pre>

Please note that you can **create your own plugin** to create your very own Reference Id(s).

To **get the the last used Reference Id**, you can call the `GetLastReferenceId()` helper method on the the `ExceptionlessClient` instance.

#### C#

<pre class="brush: csharp; title: ; notranslate" title="">using Exceptionless;
// Get the last created Reference Id
ExceptionlessClient.Default.GetLastReferenceId();</pre>

#### JavaScript

<pre class="brush: jscript; title: ; notranslate" title="">// Get the last created Reference Id
exceptionless.ExceptionlessClient.default.getLastReferenceId();
</pre>

You might have noticed how easy it is to get or add Reference Id’s to your events automatically. This makes it a breeze to let your developers track down user-facing issues by displaying the Reference Id to your end users.

We **display Reference Ids** to all of our end users anytime an error occurs in our ASP.NET WebAPI application. We accomplish this by adding a custom `<a href="http://www.asp.net/web-api/overview/error-handling/web-api-global-error-handling" target="_blank">IExceptionHandler</a>` and return a new <a href="https://github.com/exceptionless/Exceptionless/blob/master/Source/Api/Utility/Handlers/ExceptionlessReferenceIdExceptionHandler.cs#L35-L51" target="_blank">error response to include the Reference Id</a> as shown below:

<pre class="brush: csharp; title: ; notranslate" title="">public class ExceptionlessReferenceIdExceptionHandler : IExceptionHandler {
	public Task HandleAsync(ExceptionHandlerContext context, CancellationToken cancellationToken) {
		if (context == null)
			throw new ArgumentNullException(nameof(context));

		var exceptionContext = context.ExceptionContext;
		var request = exceptionContext.Request;
		if (request == null)
			throw new ArgumentException($"{typeof(ExceptionContext).Name}.{"Request"} must not be null", nameof(context));

		context.Result = new ResponseMessageResult(CreateErrorResponse(request, exceptionContext.Exception, HttpStatusCode.InternalServerError));
		return TaskHelper.Completed();
	}

	private HttpResponseMessage CreateErrorResponse(HttpRequestMessage request, Exception ex, HttpStatusCode statusCode) {
		HttpConfiguration configuration = request.GetConfiguration();
		HttpError error = new HttpError(ex, request.ShouldIncludeErrorDetail());

		string lastId = ExceptionlessClient.Default.GetLastReferenceId();
		if (!String.IsNullOrEmpty(lastId))
			error.Add("Reference", lastId);

		// CreateErrorResponse should never fail, even if there is no configuration associated with the request
		// In that case, use the default HttpConfiguration to con-neg the response media type
		if (configuration == null) {
			using (HttpConfiguration defaultConfig = new HttpConfiguration()) {
				return request.CreateResponse(statusCode, error, defaultConfig);
			}
		}

		return request.CreateResponse(statusCode, error, configuration);
	}
}</pre>

The next step is to <a href="https://github.com/exceptionless/Exceptionless/blob/master/Source/Api/AppBuilder.cs#L63" target="_blank">replace the existing <code>IExceptionFilter</code></a> with the one above.

<pre class="brush: csharp; title: ; notranslate" title="">Config.Services.Replace(typeof(IExceptionHandler), new ExceptionlessReferenceIdExceptionHandler());</pre>

Finally, when an error occurs in your app, you’ll get a more user friendly error response that contains a Reference Id!

<pre class="brush: csharp; title: ; notranslate" title="">{
  "message": "An error has occurred.",
  “reference”: “411085622e”
}</pre>

We’ve found that this allows consumers of our API to quickly contact us with a reference id and get up and running quickly!

## Looking up Events by Reference Id

You might be thinking: &#8220;Reference Ids are great, but what do I do with them now that I have one.&#8221; Well, you can view the event that they reference on our site or via our API. This can be accomplished two different ways:

* **Hotlinking
** You can link directly to a submitted event by outputting a link in your UI or logs (e.g. https://be.exceptionless.io/event/by-ref/YOUR\_REFERENCE\_ID)
* **Search
** You can search via our api/ui with `reference:YOUR_REFERENCE_ID`

## Your Turn!

We hope this article was helpful, and we'd love to know if you're using Reference Ids and how they've helped you help users, solve internal issues, etc. Post a comment below!