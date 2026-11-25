---
type: Excerpt
canonical_url: https://developer.webex.com/docs/calling-device-id-guide
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- What's New
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/calling-device-id-guide). [Full Markdown](../../../../docs/calling-device-id-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The [Webex Calling Platform](https://developer.webex.com/docs/webex-calling-overview) supports a variety of calling capable device types/products, generically referred to as devices.
Developers can better utilize device related APIs by understanding the types of device identifier (deviceId), their lifecycles, and recent improvements in the handling and presentation of device identifiers in Webex APIs.

This guide provides details about extensions of deviceId handling in a couple of APIs, and also information about the deviceId types, lifecycles, and usage.

## Selected section

## What's New

Improvements to the discovery and use of deviceIds have been made in the [List Devices API (GET /v1/devices)](https://developer.webex.com/docs/api/v1/devices/list-devices) and the [Get Device Details API (GET /v1/devices/{deviceId})](https://developer.webex.com/docs/api/v1/devices/get-device-details).

### New identifier fields reported by the [List Devices API (GET /v1/devices)](https://developer.webex.com/docs/api/v1/devices/list-devices) and the [Get Device Details API (GET /v1/devices/{deviceId})](https://developer.webex.com/docs/api/v1/devices/get-device-details)

Two new attributes have been added to the [List Devices API (GET /v1/devices)](https://developer.webex.com/docs/api/v1/devices/list-devices) and the [Get Device Details API (GET /v1/devices/{deviceId})](https://developer.webex.com/docs/api/v1/devices/get-device-details):

- `webexDeviceId` -  this field is returned when a device has a `DEVICE` type ID and is suitable for use with Webex APIs like `/v1/deviceConfiguration`.
- `callingDeviceId` - this field is returned when a device has a `CALLING_DEVICE` type ID; it can be used with Webex Calling APIs like the `/v1/telephony/config` API.

NOTE: The type and visibility of the existing `id` field in the [List Devices API (GET /v1/devices)](https://developer.webex.com/docs/api/v1/devices/list-devices) and the [Get Device Details API (GET /v1/devices/{deviceId})](https://developer.webex.com/docs/api/v1/devices/get-device-details) remains unchanged.

### New identifier type accepted by the [Get Device Details API (GET /v1/devices/{deviceId})](https://developer.webex.com/docs/api/v1/devices/get-device-details) API

When available, now, either the `DEVICE` or the `CALLING_DEVICE` type ID values can be used as {deviceId} in the [Get Device Details API (GET /v1/devices/{deviceId})](https://developer.webex.com/docs/api/v1/devices/get-device-details) API requests.
