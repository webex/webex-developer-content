---
type: Guide
title: Get Started with the Desktop SDK
display_title: Get Started with the Desktop SDK
canonical_url: https://developer.webex.com/docs/desktop-sdk-getting-started
content_type: documentation
product_group:
- webex-contact-center
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/desktop-sdk-getting-started)

Install and initialize the Desktop SDK to access Desktop modules from custom widgets.

## JavaScript SDK and Modules

**Caution:** Restrain from using old libraries such as `@agentxJsApi`, `@agentx/agentx`, `@agentx/agentx-services-types` and `@agentx/agentx-js-api`.

The references for the term `agentx` have been amended:

- `@agentx/agentx` and `@agentx/agentx-services-types` are exported under a common name `@wxcc-desktop/sdk-types`
- `@agentx/agentx-js-api` is renamed to `@wxcc-desktop/sdk`
- `agentxJsApi` is renamed to `Desktop`

For more information on using the JavaScript SDK, see [Get Started](https://developer.webex.com/docs/desktop-sdk-getting-started#get-started).

## Javascript SDK

**Caution:** The JavaScript SDK library can be used to build widgets that are embedded within the Desktop. You cannot use this library outside of the Desktop or to create a new Desktop.

**Note:** The `@wxcc-desktop/sdk-types` library does not support iFrame based widgets.

The Desktop JavaScript SDK is an npm package that allows you to request up-to-date information from the Desktop. Using the SDK, you can request information such as agent details, assigned tasks, details of specific tasks, current browser locale, and the authentication token for Single Sign-On (SSO) integration.

The SDK package allows you to:

- request data to be passed to your widgets through properties and attributes.
- perform more complex operations by consuming and manipulating the system data inside your widget.
- subscribe to data arriving asynchronously.

Some events in the Desktop occur asynchronously. To subscribe to asynchronous events and access data within the payload, you can add a listener. A few examples for asynchronous events are:

- New task offered
- New task assigned
- Consult request created
- Consult ended
- Screen pop arrived

For the complete list of asynchronous events, see [Asynchronous Events](https://developer.webex.com/docs/desktop-contact-events#asynchronous-events).

## Get Started

To start using the JavaScript SDK, you can use any of the following options:

- Run the following command in your project folder: `npm install @wxcc-desktop/sdk --save` or `yarn add @wxcc-desktop/sdk`
- Alternatively, add the following entry to your package.json file:

```json
{
"dependencies": {
    "@wxcc-desktop/sdk": "^3.0.1"
}
}
```

- If you also choose to use our Momentum-ui Web Component library, you must add:

```json
{
"peerDependencies": {
    "@momentum-ui/core": "19.9.2",
    "@momentum-ui/icons": "7.45.0",
    "@momentum-ui/utils": "6.2.7",
    "@momentum-ui/web-components": "^2.0.13",
    "lit-element": "^2.3.1",
    "lit-html": "^1.2.1"
}
}
```

In addition, to access the type definition of return Promise for the JavaScript SDK requests, install the following package:

```json
{
"devDependencies": {
    "@wxcc-desktop/sdk-types": "^1.0.2"
}
}
```

**Note:** Momentum and lit-element dependencies are added to `peerDependencies`. These dependencies are present in Desktop, and should not be imported twice. There is no way to maintain the same versions in your widget and in Desktop.

Once you have installed the package in your project, include it in the appropriate component file following the ES6 import pattern: `import {Desktop} from "@wxcc-desktop/sdk";`

## Root JavaScript SDK Module

`Desktop` is the root module of the JavaScript SDK. The root module provides a reference to the following sub-modules:

- Configuration Module
- Localization Module
- Actions Module
- Logger Module
- Agent State Information Module
- Agent Contact Module
- Dialer Module
- Screen Pop Module
- Shortcut Key Module
- Call Monitoring Module
- Webex Metrics Module
- Schedule Callback Module
- Popover Module

**Example**

```javascript
import { Desktop } from "@wxcc-desktop/sdk";

const {
  config,
  i18n,
  actions,
  agentContact,
  agentStateInfo,
  dialer,
  logger,
  screenpop,
  shortcutKey, 
  webexMetricsInternal,
  scheduleCallback,
  popover,
} = Desktop;
```

## Configuration Module

The `Desktop.config` module provides configuration details of Desktop.

**Example**

```javascript
import { Desktop } from "@wxcc-desktop/sdk";

await Desktop.config.init({ widgetName: "my-widget", widgetProvider: "cisco" });

// After Desktop config initiated, all sub-modules will inject SERVICE instance via their init() methods automatically

// Use the SDK while the widget is mounted.
```

Call `Desktop.config.cleanup()` during widget teardown, after the widget has finished using the SDK. Cleanup also cleans the submodules; do not call it immediately after startup.

If an integration or test environment reuses SDK modules with a different `SERVICE` instance, clean up the previous configuration before reinitializing them.

```javascript
function teardownWidget() {
  Desktop.config.cleanup();
}
```

### Methods

#### init(config)

Initializes the configuration module before using other `Desktop` modules. The current SDK accepts one configuration object containing `widgetName` and `widgetProvider`, as defined in the [published SDK package](https://www.npmjs.com/package/@wxcc-desktop/sdk). Initialize it inside Desktop after the widget connects.

**Version compatibility:** SDK versions before 2.0 used `Desktop.config.init()` without arguments. From version 2.0 onward, provide `widgetName` and `widgetProvider` in a single configuration object, as shown below.

**Example**

```javascript
await Desktop.config.init({
  widgetName: "my-widget",
  widgetProvider: "cisco"
});
```

For more information on the widget starter example, see [Cisco Webex Contact Center Widget Starter](https://github.com/CiscoDevNet/webex-contact-center-widget-starter).

**Parameters**

| Name           | Type   | Description                               | Required |
| -------------- | ------ | ----------------------------------------- | -------- |
| config.widgetName     | String | The name of the widget to be initialized. | Yes      |
| config.widgetProvider | String | The provider of the widget.               | Yes      |

#### registerCrmConnector()

The registerCrmConnector method is introduced as a new function to register a CRM connector. It is recommended for use when developing a connector for CRM purposes. This function allows the SDK to integrate and interact effectively with the specified CRM platform (in this example, "SFDC" with provider "Cisco").

```javascript
/** 
   crmConnectorProvider (String): The provider of the CRM connector. e.g. Cisco, B&S etc
  crmPlatform (String): The CRM platform for which the connector is registered. e.g. SFDC, ServiceNow, ZenDesk etc. */
Desktop.config.registerCrmConnector({
  crmConnectorProvider: "Cisco",
  crmPlatform: "SFDC"
});
```

**Parameters**

| Name                 | Type   | Description                                                                                 | Required |
| -------------------- | ------ | ------------------------------------------------------------------------------------------- | -------- |
| crmConnectorProvider | String | The provider or vendor that supplies the CRM connector.                                     | Yes      |
| crmPlatform          | String | The CRM platform for which the connector is registered. e.g. SFDC, ServiceNow, ZenDesk etc. | Yes      |

#### clientLocale

Requests system data such as locale of the client.

```javascript
const locale = Desktop.config.clientLocale;
```

**Returns**
`{String}` The locale of the client.

**Example Response**

```javascript
const clientLocaleResponse = "en-US";
```

## Desktop Actions

The `Desktop.actions` module retrieves data and performs actions for Desktop widgets.

### getToken()

Retrieves the authentication token used for SSO authentication.

**Example**

```javascript
const accessToken = await Desktop.actions.getToken();
// => Get current accessToken from Desktop store
```

**Returns**
`{String}` A user access token.

## Related Pages

- [Agent Desktop overview](https://developer.webex.com/docs/desktop)
- [Desktop SDK Reference](https://developer.webex.com/docs/desktop-sdk-reference)
