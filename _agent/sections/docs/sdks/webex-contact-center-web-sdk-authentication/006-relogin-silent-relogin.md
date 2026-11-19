---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-authentication
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Relogin (Silent Relogin)
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-authentication). [Full Markdown](../../../../../docs/sdks/webex-contact-center-web-sdk-authentication.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](001-prerequisites.md)

## Article introduction

This guide covers authentication; session registration and cleanup; agent station login and logout; automatic relogin; multi-login behavior; and agent state management in the Contact Center SDK.

---



> **Info**
>
> Note: For single-session apps, you can rely on method promises alone, subscribe to events mainly for multi-session support (for example, handling more than one active session).

<br>

## Selected section

## Relogin (Silent Relogin)

When `allowAutomatedRelogin` is enabled during `Webex.init`, the SDK can automatically relogin if the agent already has an active session.

#### Request Parameters

None (automatic behavior).

#### Response Payload

Delivered via the success event payload.

| key | description |
| --- | --- |
| `deviceType` | The device type the agent is logged into (`BROWSER`, `EXTENSION`, or `AGENT_DN`). |
| `dn` | The directory number used/assigned for the session (if applicable). |
| `auxCodeId` | Aux code id applied to the agent at the time of relogin. |
| `lastStateChangeTimestamp` | ISO timestamp of the last agent state change. |
| `lastIdleCodeChangeTimestamp` | ISO timestamp of the last aux code change. |

#### Success event

```javascript
webex.cc.on('agent:reloginSuccess', (data) => {
  // Automatic relogin completed; update UI (deviceType, dn, aux code, timestamps)
});
```
