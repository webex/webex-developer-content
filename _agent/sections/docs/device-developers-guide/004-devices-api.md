---
type: Excerpt
canonical_url: https://developer.webex.com/docs/device-developers-guide
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Devices API
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/device-developers-guide). [Full Markdown](../../../../docs/device-developers-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Provision, manage and control your Webex devices.

---

An integrator can use the device APIs to integrate with devices. There are four APIs that can be used to interact with devices:

- **[Devices API](https://developer.webex.com/docs/devices#devices-api)**: The inventory of your devices that can be used to view and delete devices or to create activation codes for getting new devices online.
- **[Device Configurations API](https://developer.webex.com/docs/devices#device-configurations-api)**: View and update the configurations of any device, online or offline.
- **[Workspaces API](https://developer.webex.com/docs/devices#workspaces-api)**: Create, view, update and delete workspaces. Workspaces represent where people work, such as conference rooms and meeting spaces
- **[xAPI](https://developer.webex.com/docs/devices#xapi)**: Allows developers to programmatically invoke commands and query the status of devices.

## Selected section

## Devices API

The [Devices API](https://developer.webex.com/docs/api/v1/devices) is the management API for the devices in your organization. You can use it to view some details on your devices, generate activation codes for adding new devices, or delete devices. In a device's details, you will find its *id*, which you will need to identify the device in any of the other APIs described in this guide.

### Finding the deviceId for a specific device

When calling any of the other device APIs, you always need to specify the `deviceId`.  The `deviceId` is generated when it a device is registered to the Cisco Webex cloud. It is good practice to avoid hardcoding the identifier.

Use the [GET List Devices method](https://developer.webex.com/docs/api/v1/devices/list-devices) to list devices: `GET https://webexapis.com/v1/devices/`

There are a lot of query parameters you can use to narrow down your search, see the [API reference](https://developer.webex.com/docs/api/v1/devices/list-devices) for details.

The command returns a list of devices that the authorized bot or user is entitled to see. There is one object for each device:

```json
{
    "items": [
        {
            "id": "...",
            ...
        },
        ...
    ]
}
```

Pay special attention to the following object fields:

- `id`: This is the `deviceId` that the bot or user must pass to any API call.
- `permissions`: The value of this field is an array. The bot or user can make xAPI calls only to the devices where "xapi" is part of this array. Always check the value of this field if you plan to use the xAPI, because the list of devices may also include devices that you are not permitted to make xAPI calls to.
