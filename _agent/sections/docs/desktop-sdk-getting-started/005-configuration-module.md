---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-sdk-getting-started
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Configuration Module
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-sdk-getting-started). [Full Markdown](../../../../docs/desktop-sdk-getting-started.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Install and initialize the Desktop SDK to access Desktop modules from custom widgets.

## Selected section

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
