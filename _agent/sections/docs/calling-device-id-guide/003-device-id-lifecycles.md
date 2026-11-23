---
type: Excerpt
canonical_url: https://developer.webex.com/docs/calling-device-id-guide
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Device ID Lifecycles
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/calling-device-id-guide). [Full Markdown](../../../../docs/calling-device-id-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The [Webex Calling Platform](https://developer.webex.com/docs/webex-calling-overview) supports a variety of calling capable device types/products, generically referred to as devices.
Developers can better utilize device related APIs by understanding the types of device identifier (deviceId), their lifecycles, and recent improvements in the handling and presentation of device identifiers in Webex APIs.

This guide provides details about extensions of deviceId handling in a couple of APIs, and also information about the deviceId types, lifecycles, and usage.

## Selected section

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
