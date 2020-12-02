---
title: Client Configuration Values
---
* [About](#about)
* [Usage Example](#usage-example)
* [.NET Helpers](#net-helpers)
* [Updating Client Configuration settings](#updating-client-configuration-settings)
* [Subscribing to Client Configuration Setting changes](#subscribing-to-client-configuration-setting-changes)

## About
[Read about client configuration and view in-depth examples](https://github.com/exceptionless/Exceptionless/wiki/Project-Settings#client-configuration)

## Usage Example

The below example demonstrates **how we would turn on or off log event submissions at runtime** without redeploying the app or changing server config settings.

First, we add a (completely arbitrary for this example) `enableLogSubmission` client configuration value key with value `true` in the Project's Settings in the Exceptionless dashboard.

![Exceptionless Client Configuration Value](https://camo.githubusercontent.com/8899b8a64c5b30ea58bb30ffc8a3d0f063e3293b/687474703a2f2f657863657074696f6e6c6573732e636f6d2f6173736574732f70726f6a6563742d73657474696e67732d706167652e706e67)

Then, we register a new client side plugin that runs each time an event is created. If our key (`enableLogSubmission`) is set to false and the event type is set to log, we will discard the event.

```javascript
exceptionless.ExceptionlessClient.default.config.addPlugin('Conditionally cancel log submission', 100, function (context, next) {
    var enableLogSubmission = context.client.config.settings['enableLogSubmission'];
 
    // only cancel event submission if it’s a log event and
    // enableLogSubmission is set to a value and the value is not true.
    if (context.event.type === 'log' && (!!enableLogSubmission && enableLogSubmission !== 'true')) {
       context.cancelled = true;
    }
 
    next();
});
```

***


## Updating Client Configuration settings

![Exceptionless Client Configuration Settings](https://exceptionless.com/assets/client-configuration.png)

All project settings are synced to the client in almost real time. When an event is submitted to Exceptionless we send down a response header with the current configuration version. If a newer version is available we will immediately retrieve and apply the latest configuration. 

By default the client will check after `5 seconds` on client startup (*if no events are submitted on startup*) and then every `2 minutes` after the last event submission for updated configuration settings. 
  * Checking for updated settings doesn't count towards plan limits. 
  * Only the current configuration version is sent when checking for updated settings (no user information will ever be sent). 
  * If the settings haven't changed, then no settings will be retrieved.

You can also **turn off the automatic updating of configuration settings when idle** using the code below.
```js
client.config.updateSettingsWhenIdleInterval = -1;
```

You can also manually update the configuration settings using the code below.
```js
exceptionless.SettingsManager.updateSettings(client.config);
```

## Subscribing to Client Configuration Setting changes
To be notified when client configuration settings change, subscribe to them using the below code.

```js
exceptionless.SettingsManager.onChanged(function(configuration) {
   // configuration.settings contains the new settings
});
```