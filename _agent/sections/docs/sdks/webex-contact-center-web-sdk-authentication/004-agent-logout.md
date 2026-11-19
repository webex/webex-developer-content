---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-authentication
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Agent Logout
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

## Agent Logout

```javascript
await webex.cc.stationLogout({ logoutReason: 'logout' });
```

#### Request Parameters

| key | type | required | description |
| --- | --- | --- | --- |
| `logoutReason` | string | no | Optional free-text or enumerated reason. Common value: `logout`. |

#### Response Payload

None. The operation completes when the station is logged out.

#### Success & Failure events

```javascript
webex.cc.on('agent:logoutSuccess', () => {
  // Station logout completed; update UI state
});

webex.cc.on('agent:logoutFailed', (error) => {
  // Handle failure
});
```
