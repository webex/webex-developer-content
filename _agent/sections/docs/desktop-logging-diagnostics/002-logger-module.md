---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-logging-diagnostics
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Logger Module
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-logging-diagnostics). [Full Markdown](../../../../docs/desktop-logging-diagnostics.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](001-before-you-begin.md)

## Article introduction

Create widget loggers and collect, download, and clean up Desktop widget logs.

## Selected section

## Logger Module

The `Desktop.logger` module creates and maintains the client-side log messages for third-party widgets.

With individually set up logger, you can integrate with the Desktop logging system (that is being used for telemetry and problem report) and at the same time maintain a clear origin definition. We recommend that you create a logger instance for your widgets only once per project. Create a logger instance in a utils.ts file and reuse throughout the components.

**Example**

```javascript
// utils.ts file
import { Desktop } from "@wxcc-desktop/sdk";

export const logger = Desktop.logger.createLogger("my-custom-component");

```

In `Component.ts`:

```javascript
import { logger } from "./utils.ts";

logger.info("Info test"); // logger.info => 2020-12-16 13:11:04:971["my-custom-component", "Info test"]
logger.warn("Warn test"); // logger.info => 2020-12-16 13:11:04:971["my-custom-component", "Warn test"]
logger.error("Error test"); // logger.info => 2020-12-16 13:11:04:971["my-custom-component", "Error test"]
```

For more information on the widget starter example, see [Cisco Webex Contact Center Widget Starter](https://github.com/CiscoDevNet/webex-contact-center-widget-starter/blob/master/lit-element/src/components/sdk.ts).

You can obtain logs in a JSON format or as a downloadable \*.log file specifically for your widget. The following are the available options to download the logs:

```javascript
// Download logs as a JSON file for "my-custom-component" prefix:
Desktop.logger.browserDownloadLogsJson("my-custom-component");

// Download logs as a Text file for "my-custom-component" prefix:
Desktop.logger.browserDownloadLogsText("my-custom-component");

// Get logs as Objects collection for "my-custom-component" prefix:
Desktop.logger.getLogsCollection("my-custom-component");

// Get logs as base64 encoded url ready to put into link href to initiate browser download as a JSON file for "my-custom-component" prefix:
Desktop.logger.getLogsJsonUrl("my-custom-component");

// Get logs as base64 encoded url ready to put into link href to initiate browser download as a Text file for "my-custom-component" prefix:
Desktop.logger.getLogsTextUrl("my-custom-component");

// Cleanup logs from Local Storage for "my-custom-component" prefix:
Desktop.logger.cleanupPrefixedLogs("my-custom-component");
```

You can also download logs from the Desktop. For instructions, see [Download error reports](https://help.webex.com/en-us/article/neidf/Download-error-reports) in Webex Help Center.

### Methods

#### createLogger(my-custom-component)

Initializes the logger for third-party widgets that help in logging related information to a particular component. Different methods are used based on the log type. The messages such as info, warn, and error are logged in the browser console.

**Example**

```javascript
const logerOne = Desktop.logger.createLogger("my-custom-component-one");
const logerTwo = Desktop.logger.createLogger("my-custom-component-two");

logerOne.info("Info test"); // console.log => "my-custom-component: Info:test"
logerTwo.warn("Warn test"); // console.log => "my-custom-component: Warn:test"
logerOne.error("Error test"); // console.log => "my-custom-component: Error:test"
```

**Parameters**

| Name                | Type   | Description                                                      | Required |
| ------------------- | ------ | ---------------------------------------------------------------- | -------- |
| my-custom-component | String | Name of the component. Example: email component, chat component. | Yes      |

#### browserDownloadLogsJson(my-custom-component)

Downloads logs as a JSON file for the `my-custom-component` prefix.

**Example**

```javascript
Desktop.logger.browserDownloadLogsJson("my-custom-component");
```

**Parameters**

| Name                | Type   | Description                                                      | Required |
| ------------------- | ------ | ---------------------------------------------------------------- | -------- |
| my-custom-component | String | Name of the component. Example: email component, chat component. | Yes      |

#### browserDownloadLogsText(my-custom-component)

Downloads logs as a text file for the `my-custom-component` prefix.

**Example**

```javascript
Desktop.logger.browserDownloadLogsText("my-custom-component");
```

**Parameters**

| Name                | Type   | Description                                                      | Required |
| ------------------- | ------ | ---------------------------------------------------------------- | -------- |
| my-custom-component | String | Name of the component. Example: email component, chat component. | Yes      |

#### getLogsCollection(my-custom-component)

Retrieves logs as a collection of objects for the `my-custom-component` prefix.

**Example**

```javascript
Desktop.logger.getLogsCollection("my-custom-component");
```

**Parameters**

| Name                | Type   | Description                                                      | Required |
| ------------------- | ------ | ---------------------------------------------------------------- | -------- |
| my-custom-component | String | Name of the component. Example: email component, chat component. | Yes      |

#### getLogsJsonUrl(my-custom-component)

Retrieves logs as a Base64 encoded URL to initiate browser download as a JSON file for the `my-custom-component` prefix.

**Example**

```javascript
Desktop.logger.getLogsJsonUrl("my-custom-component");
```

**Parameters**

| Name                | Type   | Description                                                      | Required |
| ------------------- | ------ | ---------------------------------------------------------------- | -------- |
| my-custom-component | String | Name of the component. Example: email component, chat component. | Yes      |

#### getLogsTextUrl(my-custom-component)

Retrieves logs as a Base64 encoded URL to initiate browser download as a text file for the `my-custom-component` prefix.

**Example**

```javascript
Desktop.logger.getLogsTextUrl("my-custom-component");
```

**Parameters**

| Name                | Type   | Description                                                      | Required |
| ------------------- | ------ | ---------------------------------------------------------------- | -------- |
| my-custom-component | String | Name of the component. Example: email component, chat component. | Yes      |

#### cleanupPrefixedLogs(my-custom-component)

Cleans up logs from the local storage for the `my-custom-component` prefix.

**Example**

```javascript
Desktop.logger.cleanupPrefixedLogs("my-custom-component");
```

**Parameters**

| Name                | Type   | Description                                                      | Required |
| ------------------- | ------ | ---------------------------------------------------------------- | -------- |
| my-custom-component | String | Name of the component. Example: email component, chat component. | Yes      |
