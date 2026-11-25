---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-authentication
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Agent State: Available and Idle (Aux Codes)'
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

## Agent State: Available and Idle (Aux Codes)

Change the agent state using `setAgentState`:

```javascript
await webex.cc.setAgentState({
  state: 'Available' | 'Idle',
  auxCodeId: '<AUX_CODE_ID>',
  lastStateChangeReason: '<FREE_TEXT_REASON>',
});
```

#### Request Parameters

| key | type | required | description |
| --- | --- | --- | --- |
| `state` | string | yes | Target state. One of `Available` or `Idle`. |
| `auxCodeId` | string | conditional | Required when `state` is `Idle`; commonly `'0'` represents Available. |
| `lastStateChangeReason` | string | no | Optional free-text reason to accompany the change. |
| `agentId` | string | no | Optional; when provided, targets a specific agent id. Defaults to the current agent. |

#### Response Payload

None. Use events to react to the resulting state.

#### Success & Failure events

```javascript
webex.cc.on('agent:stateChangeSuccess', (data) => {
  // Make UI changes as per auxCodeId and timestamps
});

webex.cc.on('agent:stateChangeFailed', (error) => {
  // Handle failure
});
```
