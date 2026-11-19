---
type: Guide
title: Calling Device ID Guide
display_title: Calling Device ID Guide
canonical_url: https://developer.webex.com/docs/calling-device-id-guide
content_type: documentation
product_group:
- webex-suite
categories:
- calling
- devices
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/calling-device-id-guide)

The [Webex Calling Platform](https://developer.webex.com/docs/webex-calling-overview) supports a variety of calling capable device types/products, generically referred to as devices.
Developers can better utilize device related APIs by understanding the types of device identifier (deviceId), their lifecycles, and recent improvements in the handling and presentation of device identifiers in Webex APIs.

This guide provides details about extensions of deviceId handling in a couple of APIs, and also information about the deviceId types, lifecycles, and usage.

## What's New

Improvements to the discovery and use of deviceIds have been made in the [List Devices API (GET /v1/devices)](https://developer.webex.com/docs/api/v1/devices/list-devices) and the [Get Device Details API (GET /v1/devices/{deviceId})](https://developer.webex.com/docs/api/v1/devices/get-device-details).

### New identifier fields reported by the [List Devices API (GET /v1/devices)](https://developer.webex.com/docs/api/v1/devices/list-devices) and the [Get Device Details API (GET /v1/devices/{deviceId})](https://developer.webex.com/docs/api/v1/devices/get-device-details)

Two new attributes have been added to the [List Devices API (GET /v1/devices)](https://developer.webex.com/docs/api/v1/devices/list-devices) and the [Get Device Details API (GET /v1/devices/{deviceId})](https://developer.webex.com/docs/api/v1/devices/get-device-details):

- `webexDeviceId` -  this field is returned when a device has a `DEVICE` type ID and is suitable for use with Webex APIs like `/v1/deviceConfiguration`.
- `callingDeviceId` - this field is returned when a device has a `CALLING_DEVICE` type ID; it can be used with Webex Calling APIs like the `/v1/telephony/config` API.

NOTE: The type and visibility of the existing `id` field in the [List Devices API (GET /v1/devices)](https://developer.webex.com/docs/api/v1/devices/list-devices) and the [Get Device Details API (GET /v1/devices/{deviceId})](https://developer.webex.com/docs/api/v1/devices/get-device-details) remains unchanged.

### New identifier type accepted by the [Get Device Details API (GET /v1/devices/{deviceId})](https://developer.webex.com/docs/api/v1/devices/get-device-details) API

When available, now, either the `DEVICE` or the `CALLING_DEVICE` type ID values can be used as {deviceId} in the [Get Device Details API (GET /v1/devices/{deviceId})](https://developer.webex.com/docs/api/v1/devices/get-device-details) API requests.

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

## Device ID Lifecycles

Devices have different deviceId types available/assigned at different points in the device's lifecycle.

### Lifecycle of a `DEVICE` ID type deviceId

The Webex `DEVICE` ID is created after the device is onboarded and when it first reaches out to the Webex system, registering as a Webex aware or Webex native device. The device saves this for use - it remains valid until the device is factory reset.

When factory reset, the device deletes the saved `DEVICE` ID. A new `DEVICE` ID will be obtained if the device re-connects to Webex.

### Lifecycle of a `CALLING_DEVICE` ID type deviceId

The `CALLING_DEVICE` ID is created when a new device is onboarded to / activated with Webex Calling.

- Devices added using MAC address onboarding get their permanent `CALLING_DEVICE` ID assigned immediately they are onboarded.
- PhoneOS and RoomOS added using activation Code onboarding get their `CALLING_DEVICE` ID assigned only when activated (when they connect to Webex Calling).
- Other devices added using activation Code onboarding get a **temporary** `CALLING_DEVICE` ID assigned immediately when they are onboarded, but the `CALLING_DEVICE` ID value is updated with a permanent value when the device activates (connects to Webex Calling).

## Device types and their associated DeviceId types

### MPP phones

MPP phones interact with Webex Calling services.
If they are Webex Aware they also interact with the broader Webex suite services.

#### MPP ID Type: `CALLING_DEVICE`

Assignment of a `CALLING_DEVICE` ID varies depending on the onboarding mechanism selected during the device Add operation.

- **MAC address onboarded**: a permanent `CALLING_DEVICE` ID is immediately assigned and available for use.
- **Activation code onboarded**: a temporary `CALLING_DEVICE` ID is immediately assigned and available for use. The temporary ID is replaced with a permanent one when the device reaches out to Webex Calling and activates.

In both cases, the Webex Calling device resources can be accessed/modified (e.g.: Lines, Line key Layout and device settings) using the `CALLING_DEVICE` ID, even before the device activates.
When activation code onboarding is selected, the temporary ID can be used to access the Webex Calling device resources until it activates. After activation, the permanent ID must be used to access the device resources.

#### MPP ID Type: `DEVICE`

A Webex `DEVICE` ID is assigned to the device only after it reaches out to Webex and successfully activates.

### RoomOS devices

RoomOS devices interact with both Webex Calling and the broader Webex suite services. RoomOS devices are added by activation code onboarding only.
The device will not show in the [List Devices API (GET /v1/devices)](https://developer.webex.com/docs/api/v1/devices/list-devices) until the device activates.

#### RoomOS ID Type: `CALLING_DEVICE`

A `CALLING_DEVICE` ID is assigned to the device when it reaches out to Webex Calling and successfully activates.
The device's Webex Calling resources cannot be accessed before the device activates.
Once the device activates and the `CALLING_DEVICE` ID is assigned, the `CALLING_DEVICE` ID can be obtained using the [Get Person Devices API (GET /v1/device-call-settings/get-person-devices)](https://developer.webex.com/docs/api/v1/device-call-settings/get-person-devices) or the [Get Workspace Devices API (GET /v1/device-call-settings/get-workspace-devices)](https://developer.webex.com/docs/api/v1/device-call-settings/get-workspace-devices), for the device's owner ID, and then locating the device details in the list returned.

#### RoomOS ID Type: `DEVICE`

A Webex `DEVICE` ID is assigned to the device when it reaches out to Webex and successfully activates.
The device's Webex resources cannot be accessed before the device activates.

### PhoneOS phones

PhoneOS devices interact with both Webex Calling and the broader Webex suite services.
For MAC address onboarded devices the device shows in the [List Devices API (GET /v1/devices)](https://developer.webex.com/docs/api/v1/devices/list-devices) as soon as it is onboarded.
For Activation code onboarded devices the device will not show in the [List Devices API (GET /v1/devices)](https://developer.webex.com/docs/api/v1/devices/list-devices) until the device activates.

#### PhoneOS ID type: `CALLING_DEVICE`

Assignment of a `CALLING_DEVICE` ID varies depending on the onboarding mechanism selected during the device Add operation.

- **MAC address onboarded**: a permanent `CALLING_DEVICE` ID is immediately assigned and available for use. The device's Webex Calling resources can be accessed/modified (e.g.: Lines, Line key Layout and device settings) using the `CALLING_DEVICE` ID, even before the device activates. 
- **Activation code onboarded**: A `CALLING_DEVICE` ID is assigned to the device only when it reaches out to Webex Calling and successfully activates. The device's Webex Calling resources cannot be accessed before the device activates.

When the device has its `CALLING_DEVICE` ID assigned, the `CALLING_DEVICE` ID can be obtained using the [Get Person Devices (GET /v1/device-call-settings/get-person-devices)](https://developer.webex.com/docs/api/v1/device-call-settings/get-person-devices) or the [Get Workspace Devices (GET /v1/device-call-settings/get-workspace-devices)](https://developer.webex.com/docs/api/v1/device-call-settings/get-workspace-devices), for the device's owner ID, and then locating the device details in the list returned.

#### PhoneOS ID Type: `DEVICE`

A Webex `DEVICE` ID is assigned to the device when it reaches out to Webex and successfully activates.
The device's Webex resources cannot be accessed before the device activates.
