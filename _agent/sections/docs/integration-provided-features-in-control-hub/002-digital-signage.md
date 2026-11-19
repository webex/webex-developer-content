---
type: Excerpt
canonical_url: https://developer.webex.com/docs/integration-provided-features-in-control-hub
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Digital Signage
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/integration-provided-features-in-control-hub). [Full Markdown](../../../../docs/integration-provided-features-in-control-hub.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Workspace integrations can also provide new functionality in Control Hub. To achieve this, integrations can mark themselves as providing **features**, which are contracts integrations can specify that they support. Integrations that provide features are highlighted on the integrations page, and when activated, they enhance functionality provided in other areas of Control Hub.

---

Control Hub supports integration-provided digital signage and Room Navigator persistent web apps. When an integration that is marked as providing digital signage is enabled, it's available as a service in the bulk and single-device digital signage configuration modals. Read more about configuring digital signage on Webex Boards, Room, and Desk series devices [here](https://help.webex.com/en-us/article/nmd8log/Enable-Digital-Signage-on-Webex-Boards,-Room,-and-Desk-Series-Devices). Similarly, integrations providing Room Navigator persistent web apps appear in the persistent web app configuration modals. Learn how to configure a persistent web app on a Room Navigator device [here](https://help.webex.com/en-us/article/ohq3u6/Configure-a-persistent-web-app-on-Webex-Room-Navigator).

## Selected section

## Digital Signage

Adding the `digital_signage` feature and the `spark-admin:devices_digital_signage` scope to a manifest grants the integration access to a new API. The new API lets the integration provide details regarding the digital signage service it provides.

For integrations providing signage, the link to this API is contained in the `signageUrl` property of the `provisioning` and `updateApproved` JWT tokens. This API allows the integration to create, read, update, and delete the digital signage configuration required by the integration.

### Add Signage Configuration

A PUT on the `signageUrl` endpoint should contain the following payload:

```json
PUT {signageUrl}
{
  "signageUrl": "... signage URL ...",
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

This makes the integration available as a digital signage provider in Control Hub.

**Configuration Details**



| Field | Required / Optional | Value space | Description |
| ----- | ------------------- | ----------- |------------ |
| `signageUrl` | Required | URL | The provider signage URL. Can contain replacement values to allow the vendor to provide device-specific content. |
| `crossLaunch` | Map | Optional | Cross-launch URLs for assigning content to devices. Shows up as actions in Control Hub. |
| `crossLaunch.assignContent` | Map | Optional | Cross-launch URL for administering devices selected in Control Hub. |
| `crossLaunch.assignContent.url` | Required | URL | The URL to post the assign content cross-launch action JWT to. |
| `crossLaunch.manageContent` | Map | Optional | Cross-launch URL for launching to the integration from the integration details page in Control Hub. |
| `crossLaunch.manageContent.url` | Required | URL | The URL to post the manage content cross-launch action JWT to. |

**Signage URL Replacement Values**

Webex can provide integrations information about the device displaying the digital signage screen by adding it to the URL.

**Example**

- URL from integration / signage provider:

`https://signage.example.com/webex?deviceId=$(deviceId)&deviceName=$(deviceName)`

- URL fetched by the device:

`https://signage.example.com/webex?deviceId=Y2lzY29...&deviceName=Board%20Room&appId=ac6b6972-538e-11ec-bf63-0242ac130002`

**Replacement Value Details**



| Replacement Value     | Description                           |
|-----------------------|---------------------------------------|
| `$(deviceId)`           | The ID of the device: `Y2lzY29...`    |
| `$(deviceName)`       | The name of the device: `Board Room`  |
| `$(deviceModel)`      | The device model: `Y2lzY29...`        |
| `$(ownerId)`          | The ID of the device's workspace      |
| `$(ownerName)`        | The name of the device's workspace    |
| `$(organizationId)`   | The organization ID: `Y2lzY29...`     |

The replacement values are resolved by the Webex backend before provisioning the URL to the devices.

Note that there is a `_cisco_app_id` URL parameter added at the end of the URL which is used internally by the Webex backend.

**Cross-launch to the Integration**

Control Hub also supports cross-launching to integrations. If the signage configuration specifies `manageContent`, an action button appears under the Actions drop-down on the integration details page that allows the administrator to launch the provider UI to do digital signage content management. If `assignContent` is specified, a button will show in the bulk and single-device digital signage modals that allows the administrator to manage signage for the selected devices. When a cross-launch is performed, a specific cross-launch JWT is sent to the URL, with the selected devices in a `devices` list:

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

### Retrieve Signage Configuration

Integrations can read the stored configuration by performing a GET on the `signageUrl`.

```json
GET {signageUrl}
{
  "signageUrl": "... signage URL ...",
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

### Update Signage Configuration

Integrations can update the digital signage configuration by performing a PUT on the JWT `signageUrl`. This automatically provisions the updated digital signage URL configuration to devices using the workspace integration for digital signage.

```json
PUT {signageUrl}
{
  "signageUrl": "... signage URL ...",
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

### Delete Signage Configuration

Integrations can delete the digital signage configuration by performing a DELETE on the JWT `signageUrl`. This removes the digital signage that was configured with the workspace integration from the devices.

```json
DELETE {signageUrl}
```
