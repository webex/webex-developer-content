---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-authorization-device-registration
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- The Error Event
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-calling-sdk-authorization-device-registration). [Full Markdown](../../../../../docs/sdks/webex-calling-sdk-authorization-device-registration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Authorization and device creation are crucial initial steps in leveraging the full capabilities of the calling SDK. Authorization ensures secure access and permissions for developers, while device creation establishes the necessary endpoint for enabling voice and video communication features in your application.

## Selected section

## The Error Event

By listening for the `error` event, the app can monitor any errors encountered during the registration process:

```js
line.on('error', (error) => {
    // Try to re-connect and/or show error to end user
}
```

This event returns an `error` payload. If this event listener is triggered, it means the line connection encountered one of the following errors:



| **Status** | **Type** | **Message** |
| --- | --- | --- |
| `inactive` | `registrationError` | Device limit exceeded. The user already logged in to a different device. |
| `inactive` | `registrationError` | Device not found. |
| `inactive` | `tokenError` | Token expired. Authentication/Authorization error. |

 An example error object is returned in JSON:

```json
{
 "status": "inactive",
 "type": "tokenError",
 "msg": "Token expired. Authentication/Authorization error."
}
```
