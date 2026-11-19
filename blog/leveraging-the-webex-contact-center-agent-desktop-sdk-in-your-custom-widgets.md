---
type: Article
title: Leveraging the Webex Contact Center Agent Desktop SDK in Your Custom Widgets
canonical_url: https://developer.webex.com/blog/leveraging-the-webex-contact-center-agent-desktop-sdk-in-your-custom-widgets
content_type: blog
date: '2024-07-30'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/leveraging-the-webex-contact-center-agent-desktop-sdk-in-your-custom-widgets)

Welcome back to our series on enhancing the Webex Contact Center experience through custom widgets! In our previous posts, we've [explored the power of custom widgets](https://developer.webex.com/blog/unlocking-the-power-of-custom-widgets-in-webex-contact-center), [developed header widgets with an RSS feed reader](https://developer.webex.com/blog/developing-with-webex-contact-center-header-widgets-an-rss-feed-reader-example), [created navigation widgets to boost agent and supervisor productivity](https://developer.webex.com/blog/enhancing-agent-productivity-by-creating-navigation-widgets-in-webex-contact-center), [bundled our widgets with Webpack](https://developer.webex.com/blog/webex-contact-center-widget-bundling-with-webpack), and [enhanced widgets with dynamic $STORE variables](https://developer.webex.com/blog/enhancing-webex-contact-center-widgets-with-dynamic-store-variables). Today, we're diving into the [Webex Contact Center Desktop SDK](https://developer.webex.com/docs/desktop#javascript-sdk-and-modules), a powerful tool that allows you to request up-to-date information from the Desktop and integrate it seamlessly into your custom widgets.

### Introduction to the Webex Contact Center Desktop SDK

The [Desktop JavaScript SDK](https://developer.webex.com/docs/desktop#javascript-sdk-and-modules) is an [npm package](https://www.npmjs.com/package/@wxcc-desktop/sdk?activeTab=readme) that provides a robust interface for interacting with the Webex Contact Center Desktop. With this SDK, you can request essential data such as agent details, assigned tasks, task specifics, browser locale, and authentication tokens for Single Sign-On (SSO) integration. This capability opens a world of possibilities for creating more dynamic and responsive embedded widgets.

### Key Features of the JS SDK

- **Native Integration into the Desktop**: Integrated seamlessly when invoked by widgets that are rendered within the Desktop application.
- **Data Requests**: Fetch data to be passed to your widgets through properties and attributes.
- **Complex Operations**: Perform advanced operations by consuming and manipulating system data within your widget.
- **Asynchronous Event Subscription**: Subscribe to asynchronous events and access data within the payload.

<br/>

### Getting Started with the SDK

To get started, you'll need to install the SDK package from npm:

```bash
npm install @wxcc-desktop/sdk
```

Once installed, you can import the SDK into your project:

```bash
import { Desktop } from '@wxcc-desktop/sdk';
```

Next, let’s take a look at some code from our sample application.

### Sample Application

The sample application provided in the [Webex Contact Center API Samples repository](https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/widget-samples/desktop-js-sdk-sample) demonstrates how to integrate and utilize the Webex Contact Center Desktop JavaScript SDK within a custom widget. This application showcases various functionalities such as initializing the SDK, fetching agent information, handling agent states, making outbound calls, updating CAD (Call Associated Data) variables, and managing interactions through events like transfers and recording pauses. The sample app is designed to help developers understand how to leverage the SDK to build robust and interactive contact center solutions, providing a comprehensive example of real-time agent interaction management and customization within a web-based interface.



    <iframe src="https://app.vidcast.io/share/embed/e98497f6-8740-4323-8805-e988af3662a3" width="100%" height="100%"
      title="Desktop JS SDK Sample Widget" frameborder="0" loading="lazy" allowfullscreen
      style="position:absolute; top:0; left: 0;border: solid; border-radius:12px;"></iframe>


<br/>

### Sample Application Code Tour

Now, let’s take a short tour through our sample application and highlight some of the features of the SDK the application is utilizing. The source code lives in the “[src/sa-ds-sdk.js](https://github.com/WebexSamples/webex-contact-center-api-samples/blob/main/widget-samples/desktop-js-sdk-sample/src/sa-ds-sdk.js)” file.

#### Importing the Library: [Line 1](https://github.com/WebexSamples/webex-contact-center-api-samples/blob/main/widget-samples/desktop-js-sdk-sample/src/sa-ds-sdk.js#L1)

Initializes the SDK for use within the widget.
```javascript
import { Desktop } from '@wxcc-desktop/sdk';
```

#### Initialization and Setup: [Line 294](https://github.com/WebexSamples/webex-contact-center-api-samples/blob/main/widget-samples/desktop-js-sdk-sample/src/sa-ds-sdk.js#L294)

Initializes the SDK for use within the widget.

```javascript
Desktop.config.init();
```

#### Fetching Agent Information: [Line 366](https://github.com/WebexSamples/webex-contact-center-api-samples/blob/main/widget-samples/desktop-js-sdk-sample/src/sa-ds-sdk.js#L366)

Retrieves the latest data about the current agent and logs it.

```javascript
const latestData = Desktop.agentStateInfo.latestData;
```

#### Retrieving Task Information: [Line 373](https://github.com/WebexSamples/webex-contact-center-api-samples/blob/main/widget-samples/desktop-js-sdk-sample/src/sa-ds-sdk.js#L373)

Fetches the interaction ID and other task-related information from the current task map.

```javascript
const currentTaskMap = await Desktop.actions.getTaskMap();
```

#### Initiating a Transfer: [Line 393-404](https://github.com/WebexSamples/webex-contact-center-api-samples/blob/main/widget-samples/desktop-js-sdk-sample/src/sa-ds-sdk.js#L393-L404)

Initiates a transfer to a specified virtual team (vteam) using the interaction ID.

```javascript
await Desktop.agentContact.vteamTransfer
```

#### Pausing Recording: [Line 409](https://github.com/WebexSamples/webex-contact-center-api-samples/blob/main/widget-samples/desktop-js-sdk-sample/src/sa-ds-sdk.js#L409)
Pauses the recording for a given interaction using the interaction ID.

```javascript
await Desktop.agentContact.pauseRecording
```

#### Making an OutDial Call: [Line 420-439](https://github.com/WebexSamples/webex-contact-center-api-samples/blob/main/widget-samples/desktop-js-sdk-sample/src/sa-ds-sdk.js#L420-L439)

Initiates an outbound call to a specified destination using the provided entry point ID.

```javascript
await Desktop.dialer.startOutdial
```

#### Updating CAD Variables: [Line 443-461](https://github.com/WebexSamples/webex-contact-center-api-samples/blob/main/widget-samples/desktop-js-sdk-sample/src/sa-ds-sdk.js#L443-L461)

Updates the CAD (Call Associated Data) variables for a given interaction.

```javascript
await Desktop.dialer.updateCadVariables
```

#### Changing Agent State: [Line 464-486](https://github.com/WebexSamples/webex-contact-center-api-samples/blob/main/widget-samples/desktop-js-sdk-sample/src/sa-ds-sdk.js#L464-L486)

Changes the agent's state to either 'Available' or 'Idle' and updates the UI accordingly.

```javascript
await Desktop.agentStateInfo.stateChange
```

#### Subscribing to Agent Contact Events: [Line 489-508](https://github.com/WebexSamples/webex-contact-center-api-samples/blob/main/widget-samples/desktop-js-sdk-sample/src/sa-ds-sdk.js#L489-L508)

Subscribes to various agent contact [events](https://developer.webex.com/docs/desktop#asynchronous-events) to handle actions like wrap-up, hold, and unhold.

```javascript
Desktop.agentContact.addEventListener
```

### Conclusion

The Webex Contact Center Agent Desktop SDK is a powerful tool that enables developers to create more dynamic, responsive, and context-aware widgets. By leveraging methods to fetch access tokens and agent information, and subscribing to asynchronous events, you can significantly enhance the functionality and user experience of your custom widgets

Stay tuned for more insights and examples in our ongoing series on developing with Webex Contact Center. As always, we encourage you to explore the [SDK documentation](https://developer.webex.com/docs/desktop#javascript-sdk-and-modules)!

### Need Some Help? We Got You Covered!

We are excited to provide you with support for these features. If you need help, the [Webex Developer Support Team](https://developer.webex.com/support) is standing by and happy to assist. You can also start or join a conversation on the [Webex for Developers Community Forum](https://cs.co/WebexDeveloperCommunity).
