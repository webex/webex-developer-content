---
type: Excerpt
canonical_url: https://developer.webex.com/docs/devices
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Workspace Locations API
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

## Workspace Locations API

The Workspace Locations API is the management API for the locations of your organization. A Workspace Location is a physical location with a name, address, country, city, latitude and longitude. Locations can have floors with a display name and a floor number.

### Creating a workspace location

Using the POST /workspaceLocations endpoint, we can create a new location, populating the location `displayName`, `address`, `countryCode` (ISO 3166-1), `latitude` and `longitude` in the request payload. Additionally, there are optional fields supported in POST, such as `cityName` and `notes`.

```json
{
    "displayName":"Cisco Barcelona",
    "address":"Carrer de Pere IV, Barcelona, Spain",
    "countryCode":"ES",
    "cityName":"Barcelona",
    "latitude":41.4066147,
    "longitude":2.2007173,
    "notes":"A note about the location"
}
```

A location `id` is automatically assigned each time a new location is created, and the response object will contain that `id`:

```json
{
    "id": "Y2lzY29z...",
    "displayName":"Cisco Barcelona",
    "address":"Carrer de Pere IV, Barcelona, Spain",
    "countryCode":"ES",
    "cityName":"Barcelona",
    "latitude":41.4066147,
    "longitude":2.2007173,
    "notes":"A note about the location"
}
```

### Editing a workspace location

You can update details for a location by specifying the `locationId` in the location `id` parameter in the URI.  Use the endpoint
 PUT /workspaceLocations/{locationId} to edit a location, populating all details that are present in a GET request for the location details.

Request:

```json
{
    "id":"Y2lzY29z...",
    "displayName":"Cisco Barcelona",
    "address":"Carrer de Pere IV, Barcelona, Spain",
    "countryCode":"ES",
    "cityName":"Barcelona",
    "latitude":41.4066147,
    "longitude":2.2007173,
    "notes":"A new note about the location"
}
```

If you don’t include the optional `cityName` and `notes` fields, they will be reset to their default values.

Response:

```json
{
    "id":"Y2lzY29z...",
    "displayName":"Cisco Barcelona",
    "address":"Carrer de Pere IV, Barcelona, Spain",
    "countryCode":"ES",
    "cityName":"Barcelona",
    "latitude":41.4066147,
    "longitude":2.2007173,
    "notes":"A new note about the location"
}
```

### Creating a workspace location floor

Using the POST /workspaceLocations/{locationId}/floors endpoint, we can create a new floor, populating the `floorNumber` field in the request payload. Additionally, there is an optional field `displayName` supported in POST. If you don’t define the optional `displayName` field, it will not be included in the floor object.

```json
{
    "floorNumber":1,
    "displayName":"My custom name"
}
```

A floor `id` is automatically assigned each time a new floor is created, and the response object will contain that `id`:

```json
{
    "id":"Y2lzY29z...",
    "locationId": "YL34GrT...",
    "floorNumber":1,
    "displayName":"My custom name"
}
```

### Editing a workspace location floor

You can update details for a floor by specifying the `floorId` in the floor `id` parameter in the URI.  Use the endpoint PUT /workspaceLocations/{locationId}/floors/{floorId} to edit a floor, populating all details that are present in a GET request for the floor details.

Request:

```json
{
    "floorNumber":2,
    "displayName":"My custom name"
}
```

If you don’t define the optional `displayName` field, it will not be included in the floor object.

Response:

```json
{
    "id":"Y2lzY29z...",
    "locationId": "YL34GrT...",
    "floorNumber":2,
    "displayName":"My custom name"
}
```
