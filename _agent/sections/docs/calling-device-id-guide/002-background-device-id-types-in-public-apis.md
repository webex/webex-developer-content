---
type: Excerpt
canonical_url: https://developer.webex.com/docs/calling-device-id-guide
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Background: Device ID types in Public APIs'
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/calling-device-id-guide). [Full Markdown](../../../../docs/calling-device-id-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The [Webex Calling Platform](https://developer.webex.com/docs/webex-calling-overview) supports a variety of calling capable device types/products, generically referred to as devices.
Developers can better utilize device related APIs by understanding the types of device identifier (deviceId), their lifecycles, and recent improvements in the handling and presentation of device identifiers in Webex APIs.

This guide provides details about extensions of deviceId handling in a couple of APIs, and also information about the deviceId types, lifecycles, and usage.

## Selected section

## Background: Device ID types in Public APIs

### Types of Device ID

Device IDs in public APIs can be categorized as

- `DEVICE`
- `CALLING_DEVICE`
- `PERIPHERAL`

Devices can have more than one ID type. Each device can have, at most, one ID of a given device type. For example, a device may have both a `DEVICE` ID and a `CALLING_DEVICE` ID, but it can only have one of each.

### Public Device ID Examples

The general format of Webex IDs including deviceIds can be found in the What the Base? [Decoding Webex API IDs Blog](https://developer.webex.com/blog/what-the-base-decoding-webex-api-ids). The deviceId includes _type prefix_ and the _UUID_ of the specific device.

#### DEVICE type IDs

`DEVICE` type IDs are available for devices known by and interacting with Webex suite services. They are used in Public APIs to identify RoomOS and PhoneOS devices for device configuration (`/v1/deviceConfiguration`).
`DEVICE` type IDs are only available for RoomOS, PhoneOS and Webex Aware devices.

- The `id` field in the [List Devices API (GET /v1/devices)](https://developer.webex.com/docs/api/v1/devices/list-devices) can be a `DEVICE` type ID.  
- The `webexDeviceId` field, when present in the response from the [List Devices API (GET /v1/devices)](https://developer.webex.com/docs/api/v1/devices/list-devices) is a `DEVICE` type ID.

#### CALLING_DEVICE type IDs

`CALLING_DEVICE` type IDs are available for devices known by and interacting with Webex Calling. They are used in Public APIs to identify RoomOS, PhoneOS, MPP and even customer-managed and partner-managed devices.
Webex Calling device configuration requires the deviceId to be a `CALLING_DEVICE` ID.
Webex Calling device configuration is supported for RoomOS, PhoneOS and MPP; Webex Calling device configuration is not available for customer-managed nor partner-managed devices.
A `CALLING_DEVICE` ID is required for configuring lines and line key layout on Cisco managed devices, and for configuring device settings on Cisco managed MPP devices (`/v1/telephony/config`).

- The `id` field in the [List Devices API (GET /v1/devices)](https://developer.webex.com/docs/api/v1/devices/list-devices) can be a `CALLING_DEVICE` type ID.
- The `callingDeviceId` field, when present in the response from the [List Devices API (GET /v1/devices)](https://developer.webex.com/docs/api/v1/devices/list-devices) is a `CALLING_DEVICE` type ID.
  
#### PERIPHERAL type IDs

`PERIPHERAL` type IDs are available for device peripherals known by and interacting with Webex suite services. They are used in public APIs to identify peripherals (typically peripherals to RoomOS systems) such as a TV, touch screen, headset etc.
