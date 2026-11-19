---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-authorization-device-registration
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Deregister a Device
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-calling-sdk-authorization-device-registration). [Full Markdown](../../../../../docs/sdks/webex-calling-sdk-authorization-device-registration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Authorization and device creation are crucial initial steps in leveraging the full capabilities of the calling SDK. Authorization ensures secure access and permissions for developers, while device creation establishes the necessary endpoint for enabling voice and video communication features in your application.

## Selected section

## Deregister a Device

You can derigister a registered device using the `line` object's `deregister()` method:

```js
line.deregister();
```



| **Asynchronous** | No |
| --- | --- |
| **Parameters** | No parameters required |
| **Returns** | undefined |



> **Info**
>
> The `deregister()` method only begins the registration process. It does not mean that deregistration is complete.




### Determine if Deregistration is Successful

The `deregister` method only begins the registration process. To verify that the device registration is successful, register a callback to listen for the `unregistered` event:

```js
line.on('unregistered', () => {
    // Add any action that should happen after a line is unregistered
}
```



> **Info**
>
> The event subscription must happen before making the `deregister()` call.
