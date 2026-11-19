---
type: Excerpt
canonical_url: https://developer.webex.com/docs/devices
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Workspaces API
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/devices). [Full Markdown](../../../../docs/devices.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Provision, manage and control your Webex devices.

---

An integrator can use the device APIs to integrate with devices. There are four APIs that can be used to interact with devices:

- **[Devices API](https://developer.webex.com/docs/devices#devices-api)**: The inventory of your devices that can be used to view and delete devices or to create activation codes for getting new devices online.
- **[Device Configurations API](https://developer.webex.com/docs/devices#device-configurations-api)**: View and update the configurations of any device, online or offline.
- **[Workspaces API](https://developer.webex.com/docs/devices#workspaces-api)**: Create, view, update and delete workspaces. Workspaces represent where people work, such as conference rooms and meeting spaces
- **[xAPI](https://developer.webex.com/docs/devices#xapi)**: Allows developers to programmatically invoke commands and query the status of devices.

## Selected section

## Workspaces API

The [Workspaces API](https://developer.webex.com/docs/api/v1/workspaces) is the management API for the workspaces in your organization. You can use it to
 view and update details on your workspaces, to create new workspaces or to delete workspaces.

### Creating a workspace and adding a device

Using the [POST /workspaces](https://developer.webex.com/docs/api/v1/workspaces/create-a-workspace) endpoint, we can create a new workspace, populating the workspace `name`, `type` and `capacity` in the request payload. Additionally, there are optional fields supported in POST, such as `workspaceLocationId`, `floorId`, `calling`, `calendar`, `supportedDevices` and `notes`. The `workspaceLocationId` must be provided when the `floorId` is set. Only `freeCalling`, `webexEdgeForDevices`, `hybridCalling` and `webexCalling` calling types can be assigned via a POST request; the other calling types are configured via other mechanisms. If you do not choose a specific calling type, `freeCalling` will be your default. For calendar types, you can use `none`, `google` and `microsoft`. If you do not choose a specific calendar type, `none` will be set as the default. If you do not specify what devices are supported for the workspace, `collaborationDevices` will be set as the default. Give context to your workspaces with the `notes` field:

```json
{
    "displayName": "Conference Room",
    "workspaceLocationId":"YL34GrT...",
    "floorId":"Y2lzY29z...",
    "type": "meetingRoom",
    "capacity": 20,
    "calling": {
      "type": "webexCalling",
      "webexCalling":{
            "phoneNumber":"+12145652892",
            "extension":"64832",
            "locationId":"Y2lzY29..."
        }
     },
    "calendar": {
      "type": "microsoft",
      "emailAddress": "email@example.com"
    },
    "notes": "This is a note.",
    "supportedDevices": "phones"
}
```

A workspace `id` is automatically assigned each time a new workspace is created, and the response object will contain that `id`:

```json
{
    "id": "12345",
    "workspaceLocationId":"YL34GrT...",
    "floorId":"Y2lzY29z...",
    "displayName": "Conference Room",
    "type": "meetingRoom",
    "capacity": 20,
    "calling": {
      "type": "freeCalling"
    },
    "calendar": {
      "type": "microsoft",
      "emailAddress": "email@example.com"
    },
    "notes": "This is a note.",
    "supportedDevices": "phones"
}
```

Having created a new workspace, you can pass the `workspaceId` as `id` to the [Device Activation Code endpoint](https://developer.webex.com/docs/api/v1/devices/create-a-device-activation-code) (here called `placeId`) in order to generate a code that can be used to register a device to the workspace.

### Editing a workspace

You can update details for a workspace by specifying the `workspaceId` in the workspace `id` parameter in the URI.  Use the endpoint 
[PUT /workspaces](https://developer.webex.com/docs/api/v1/workspaces/update-a-workspace) to edit a workspace, populating all details that are present in a
[GET request for the workspace details](https://developer.webex.com/docs/api/v1/workspaces/get-workspace-details). Only `freeCalling`,  `hybridCalling` and  `webexCalling` calling types can be updated. The `locationId` field cannot be updated, but it must be present when updating the `webexCalling` phone number or extension fields.

Request:

```json
{
    "id": "12345",
    "displayName": "Conference Room",
    "workspaceLocationId":"YL34GrT...",
    "calling": {
      "type": "webexCalling",
      "webexCalling":{
            "phoneNumber":"+12145652892",
            "extension":"64832",
            "locationId":"Y2lzY29..."
        }
     },
    "floorId":"Y2lzY29z...",
    "type": "meetingRoom",
    "capacity": 10,
    "notes": "This is a new note."
}
```

If you don’t include the optional fields, they will be reset to their default values. The `workspaceLocationId`, `floorId`, 
`calendar` and `calling` fields do not change when omitted from the update request. The `workspaceLocationId` must be provided when 
the `floorId` is set.

Response:

```json
{
    "id": "12345",
    "workspaceLocationId":"YL34GrT...",
    "floorId":"Y2lzY29z...",
    "displayName": "Conference Room",
    "type": "meetingRoom",
    "capacity": 10,
    "calling": {
      "type": "freeCalling"
       },
    "calendar": {
      "type": "microsoft",
      "emailAddress": "email@example.com"
       },
    "notes": "This is a new note.",
    "supportedDevices": "phones"
}
```
