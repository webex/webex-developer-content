---
type: Excerpt
canonical_url: https://developer.webex.com/docs/calling-device-id-guide
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Device types and their associated DeviceId types
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/calling-device-id-guide). [Full Markdown](../../../../docs/calling-device-id-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The [Webex Calling Platform](https://developer.webex.com/docs/webex-calling-overview) supports a variety of calling capable device types/products, generically referred to as devices.
Developers can better utilize device related APIs by understanding the types of device identifier (deviceId), their lifecycles, and recent improvements in the handling and presentation of device identifiers in Webex APIs.

This guide provides details about extensions of deviceId handling in a couple of APIs, and also information about the deviceId types, lifecycles, and usage.

## Selected section

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
