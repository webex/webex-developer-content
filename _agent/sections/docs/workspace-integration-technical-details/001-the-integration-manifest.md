---
type: Excerpt
canonical_url: https://developer.webex.com/docs/workspace-integration-technical-details
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- The Integration Manifest
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/workspace-integration-technical-details). [Full Markdown](../../../../docs/workspace-integration-technical-details.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This guide describes the technical details and syntax for the manifest, OAuth, and notification messages.

---

Follow the steps below to set up a new `org_private` Workspace Integration. Every step is detailed further below in this guide.

1. Describe the application in a manifest file and upload it in Control Hub. This gives you an OAuth client ID and a client secret. For further details, see [The Integration Manifest](https://developer.webex.com/docs/workspace-integration-technical-details#the-integration-manifest) for information regarding the manifest, and [Deployment](https://developer.webex.com/docs/workspace-integration-technical-details#deployment) to make the integration available for customers to activate.
2. Receive an activation JWT. If the manifest specified the manual provisioning flow, this happens by an admin activating the integration in Control Hub and copy-pasting the JWT to your integration, as described in [Activation](https://developer.webex.com/docs/workspace-integration-technical-details#activation).
3. Use the OAuth credentials from step 1 and the credentials from step 2 to update the integration status, as described in step 4 of [Activation](https://developer.webex.com/docs/workspace-integration-technical-details#activation).

    At this point, you have everything you need to start interacting with the Webex APIs.

4. Implement the rest of the Workspace Integrations protocol.
5. Use your credentials to interact with the Webex APIs in order to implement your functionality.

To create a _public_ integration there are some additional steps, such as that the manifest needs to be approved and deployed by Cisco, as detailed in the sections below.



> **Info**
>
> Analytics, Meeting and XSI scopes do not currently work with Workspace Integrations.

## Selected section

## The Integration Manifest

The integration manifest provides the metadata needed to understand the capabilities of the integration, what permissions it needs and how it should be provisioned. Let's have a look at an example and break down the fields:

### Example Manifest

```json
{
  "id": "ac6b6972-538e-11ec-bf63-0242ac130002",
  "manifestVersion": 1,
  "displayName": "ACME Device Integration",
  "vendor": "ACME INC.",
  "email": "example-app@example.com",
  "description": "The ACME integration will do magic with your Webex device sensor data",
  "descriptionUrl": "https://example.com/webexintegration/details",
  "tocUrl": "https://example.com/webexintegration/toc",
  "availability": "global",
  "apiAccess": [
    {
      "scope": "spark-admin:devices_read",
      "access": "required",
      "role": "id_readonly_admin"
    },
    {
      "scope": "spark-admin:workspaces_read",
      "access": "required",
      "role": "id_readonly_admin"
    },
    {
      "scope": "spark:xapi_statuses",
      "access": "required"
    },
    {
      "scope": "spark:xapi_commands",
      "access": "required"
    }
  ],
  "xapiAccess": {
    "status": [
      {
        "path": "RoomAnalytics.*",
        "access": "required"
      },
      {
        "path": "Peripherals.ConnectedDevice[*].RoomAnalytics.*",
        "access": "required"
      },
      {
        "path": "Standby.State",
        "access": "required"
      },
      {
        "path": "SystemUnit.State.NumberOfActiveCalls",
        "access": "required"
      }
    ],
    "commands": [
      {
        "path": "Message.Send",
        "access": "required"
      }
    ],
    "events": [
      {
        "path": "BootEvent",
        "access": "required"
      },
      {
        "path": "UserInterface.Message.Prompt.Response",
        "access": "required"
      }
    ]
  },
  "provisioning": {
    "type": "manual"
  }
}
```

This example describes an integration from ACME, INC. It's a _global_ integration, which means it will have to be approved and deployed by Cisco, and thus made available to any customer that wants to activate it. For customers building their own integrations, the _availability_ field would be set to _org_private_, allowing the manifest to be uploaded in Control Hub.

The _apiAccess_ shows four required scopes, that would give access to reading device and workspace details, reading statuses and executing commands for the Webex Devices over the [xAPI](https://roomos.cisco.com/docs/Introduction.md#the-xapi). The status, command and event details are specified in the _xapiAccess_. The example is requesting access to:

- All status under RoomAnalytics for both the device itself and the attached peripherals (like the Room Navigator), the device standby state and how many active calls the device has.
- The UserInterface.Message.Prompt.Display command that displays a prompt on the device screen with a title, text and up to five options for the user.
- Two events: the boot event that is sent when a device reboots and the UserInterface.Message.Prompt.Response following a selection by the user for the message prompt.

The provisioning section shows that the integration is deploy type _manual_, which means the Control Hub admin will need to copy an activation code and provide this to the integration.

This is how the manifest will render in Control Hub:

![Control Hub manifest](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltea3a7c98898ec5ee/64526bc5f1b32a119f435022/control-hub-manifest.png)

### Manifest Details



| Field | Required / Optional | Value space | Description |
| ----- | ------------------- | ----------- |------------ |
| `id` | Required | UUID | The Id of the integration. Generated by the integration developer, needs to be globally unique. |
| `manifestVersion` | Required | Integer | The manifest version. When the manifest changes, the version must be incremented. |
| `displayName` | Required | String | A display name for the integration |
| `vendor` | Required | String | The name of the vendor / company that created the integration |
| `email` | Required | String | An email address from the integration vendor |
| `description` | Required | String | A description of what the integration does and what value it will provide to the customer |
| `descriptionUrl` | Optional | String | A URL to a more detailed description of what the integration does and what value it provides to the customer |
| `tocUrl` | Required (when `global`) | URL | A URL to a web page listing the terms and conditions for the integration. The admin will have to accept these when enabling the integration from Control Hub. Note that this URL is not required for private integrations.
| `availability` | Required | `global` or `org_private` | Describes if the integration is `global` and available to all customers, or `org_private`, which means it only applies to a specific customer organization. Note that only `org_private` integrations can be manually uploaded by a Control Hub admin. `global` integrations are deployed by Cisco on behalf of the vendor. |
| `apiAccess` | Required | Array| A list of Webex API scopes the integration is requesting. These scopes allow access to specific public [Webex developer APIs](https://developer.webex.com/docs/getting-started). |
| `apiAccess.scope` | Required | String | The scope requested. See [Webex API scopes](https://developer.webex.com/docs/integrations#scopes) for examples. |
| `apiAccess.access`| Required | `required` or `optional` | Is the scope required or optional. Optional scopes can be opted out by the Control Hub admin. |
| `apiAccess.role` | Optional | `id_full_admin`, `id_readonly_admin` or `id_device_admin` | Some APIs require a specific use role to be assigned to the account created for the integration. For most read APIs, `id_readonly_admin` should be sufficient. Check the API docs for the specific APIs to see what roles, if any, are required. |
| `xapiAccess` | Required | Array | A list of device xAPI status, commands and events that the integration is requesting access to. See https://roomos.cisco.com/xapi for more details of what is supported by the Webex Devices |
| `xapiAccess.status.path` | Required | String | The status path requested. Wildcards indicate all statuses recursively under the specific path, say RoomAnalytics.* means all statuses under the RoomAnalytics node in the status tree.  |
| `xapiAccess.status.access`| Required | `required` or `optional` | Is the status required or optional? Optional statuses can be opted out by the Control Hub admin. |
| `xapiAccess.commands.path` | Required | String | The command(s) requested. Wildcards indicate all commands recursively under the specific path, say Bookings.* means all commands under the Bookings node in the command tree.  |
| `xapiAccess.commands.access` | Required | `required` or `optional` | Is the command required or optional. Optional commands can be opted out by the Control Hub admin. |
| `xapiAccess.events.path` | Required | String | The event requested. |
| `xapiAccess.events.access`| Required | `required` or `optional` | Is the event required or optional? Optional events can be opted out by the Control Hub admin. |
| `provisioning` | Required | Provisioning | Describes how the integration is provisioned when enabled from Control Hub |
| `provisioning.type` | Required | `manual` or `https` | `manual` provisioning means the Control Hub admin will be presented with an activation code that is copied and provided to the integration. `https` provisioning removes the need for the activation code but requires a global activation URL for the 3rd party service. More details on this later. |
| `provisioning.url` | Required (when `https`) | URL | If the type is `manual`, the URL is optional. If set, it provides a link to the page where the admin needs to provide the activation code. If the type is `https`, the URL is required and is where the activation code is posted to start the activation flow. Note that the URL must be an HTTPS URL.  |
| `provisioning.activationGuideUrl` | Optional | URL | Cannot be used together with `provisioning.url`. If specified, it provides a link to a documentation page by the integrator explaining how to continue the activation process. |
