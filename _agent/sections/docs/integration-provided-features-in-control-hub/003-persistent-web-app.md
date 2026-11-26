---
type: Excerpt
canonical_url: https://developer.webex.com/docs/integration-provided-features-in-control-hub
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Persistent Web App
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/integration-provided-features-in-control-hub). [Full Markdown](../../../../docs/integration-provided-features-in-control-hub.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Workspace integrations can also provide new functionality in Control Hub. To achieve this, integrations can mark themselves as providing **features**, which are contracts integrations can specify that they support. Integrations that provide features are highlighted on the integrations page, and when activated, they enhance functionality provided in other areas of Control Hub.

---

Control Hub supports integration-provided digital signage and Room Navigator persistent web apps. When an integration that is marked as providing digital signage is enabled, it's available as a service in the bulk and single-device digital signage configuration modals. Read more about configuring digital signage on Webex Boards, Room, and Desk series devices [here](https://help.webex.com/en-us/article/nmd8log/Enable-Digital-Signage-on-Webex-Boards,-Room,-and-Desk-Series-Devices). Similarly, integrations providing Room Navigator persistent web apps appear in the persistent web app configuration modals. Learn how to configure a persistent web app on a Room Navigator device [here](https://help.webex.com/en-us/article/ohq3u6/Configure-a-persistent-web-app-on-Webex-Room-Navigator).

## Selected section

## Persistent Web App

Managing the Persistent Web App (PWA) configuration requires the `persistent_web_app` feature entry and the `spark-admin:devices_pwa` scope. The link to the PWA configuration API is contained in the `pwaUrl` property of the `provisioning` and `updateApproved` JWT tokens. This API allows the integration to create, read, update, and delete the PWA configuration.

### Add Persistent Web App Configuration

To configure PWA, perform a PUT on the `pwaUrl` endpoint with the following payload:

```json
PUT {pwaUrl}
{
  "pwaUrl": "... PWA URL ...",
  "crossLaunch": {
    "manageContent": {
      "url": "... cross-launch URL to manage content ..."
    },
    "assignContent": {
      "url": "... cross-launch URL to assign content ..."
    }
  }
}
```

This makes the integration available as a PWA provider in Control Hub.

Integrations can also require access to JSXAPI by adding the `spark-admin:devices_pwa_jsxapi` scope. This will allow the integration to directly access a subset of the device's xAPI when running as a persistent web app, irrespective of the permissions granted to the integration itself. This is useful for applications where low latency is required (e.g. controlling the device's LED light). [Learn more about JSXAPI](https://roomos.cisco.com/doc/TechDocs/WebAppsOnNavigator).

**Configuration Details**



| Field | Required / Optional | Value space | Description |
| ----- | ------------------- | ----------- |------------ |
| `pwaUrl` | Required | URL | The provider PWA URL. Can contain replacement values to allow the vendor to provide device-specific content. |
| `crossLaunch` | Map | Optional | Cross-launch URLs for assigning content to devices. Shows up as actions in Control Hub. |
| `crossLaunch.assignContent` | Map | Optional | Cross-launch URL for administering devices selected in Control Hub. |
| `crossLaunch.assignContent.url` | Required | URL | The URL to post the assign content cross-launch action JWT to. |
| `crossLaunch.manageContent` | Map | Optional | Cross-launch URL for launching to the integration from the integration details page in Control Hub. |
| `crossLaunch.manageContent.url` | Required | URL | The URL to post the manage content cross-launch action JWT to. |

**Persistent Web App URL Replacement Values**

Webex can provide integrations information about the Room Navigator displaying the persistent web app by adding it to the URL.

**Example**

- URL from integration / PWA provider:

`https://pwa.example.com/webex?deviceId=$(deviceId)&deviceName=$(deviceName)`

- URL fetched by the device:

`https://pwa.example.com/webex?deviceId=Y2lzY29...&deviceName=Board%20Room&appId=ac6b6972-538e-11ec-bf63-0242ac130002`

**Replacement Value Details**



| Replacement Value | Description |
| ----- | ------------------- |
| `$(deviceId)` | The ID of the device: `Y2lzY29...` |
| `$(deviceName)` | The name of the device: `Board Room` |
| `$(deviceModel)` | The device model: `Y2lzY29...` |
| `$(ownerId)` | The ID of the device's workspace |
| `$(ownerName)` | The name of the device's workspace |
| `$(peripheralSerial)` | The serial number of the Room Navigator displaying the persistent web app. | 
| `$(organizationId)` | The organization ID: `Y2lzY29...` |

The replacement values are resolved by the Webex backend before provisioning the URL to the devices.

Note that there is a `_cisco_app_id` URL parameter added at the end of the URL which is used internally by the Webex backend.

**Cross-launch to the integration**

Control Hub also supports cross-launching to integrations. If the PWA configuration specifies `manageContent`, an action button appears under the Actions drop-down on the integration details page that allows the administrator to launch the provider UI to do content management. If `assignContent` is specified, a button will show in the bulk and single-device PWA modals that allows the administrator to manage PWA for the selected devices. When a cross-launch is performed, a specific cross-launch JWT is sent to the URL, with the selected devices in a `devices` list:

```json
POST {crossLaunch.assignContent.url}
{
  "jwt": "eyJhbGciOiJSUzI1NiJ9....",
  "devices": [
    {
      "deviceId": "Y2lzY29..."
    }
  ]
}

JWT
{
  "sub": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi8zYTZmZjM3My02OGE3LTQ0ZTQtOTFkNi1hMjc0NjBlMGFjNWM",
  "iat": 1516239022,
  "jti": "WTJselkyOXpjR0Z5YXpvdkw=",
  "appId": "6d93fe09-7130-4507-b261-3908b63428a4",
  "action": "crossLaunch"
}

Response:
{
  "redirectUrl": "... required redirectUrl that will be opened in a new tab by Control Hub ... ",
}
```

### Retrieve Persistent Web App Configuration

Integrations can read the stored configuration by performing a GET on the `pwaUrl`.

```json
GET {pwaUrl}
{
  "pwaUrl": "... signage URL ...",
  "crossLaunch": {
    "manageContent": {
      "url": "... cross-launch URL to manage content ..."
    },
    "assignContent": {
      "url": "... cross-launch URL to assign content ..."
    }
  }
}
```

### Update Persistent Web App Configuration

Integrations can update the PWA configuration by performing a PUT on the JWT `pwaUrl`. This automatically provisions the updated PWA URL configuration to devices using the workspace integration for PWA.

```json
PUT {pwaUrl}
{
  "signageUrl": "... PWA URL ...",
  "crossLaunch": {
    "manageContent": {
      "url": "... cross-launch URL to manage content ..."
    },
    "assignContent": {
      "url": "... cross-launch URL to assign content ..."
    }
  }
}
```

### Delete Persistent Web App Configuration

Integrations can delete the PWA configuration by performing a DELETE on the JWT `pwaUrl`. This removes the PWA that was configured with the workspace integration from the devices.

```json
DELETE {pwaUrl}
```
