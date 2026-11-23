---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-tasks
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Outbound Dialing (Telephony)
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-tasks). [Full Markdown](../../../../../docs/sdks/webex-contact-center-web-sdk-tasks.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This page documents how to work with tasks using only public SDK methods and events.

---



> **Info**
>
> It is necessary to listen to all task events only if your application supports multi-session usage (i.e., the same agent is signed in from multiple tabs, windows, or devices). For single-session applications, promise-based method responses are sufficient for most scenarios, and you typically only need to subscribe to a select set of events. The specific events required are indicated in the relevant sections below.

## Selected section

## Outbound Dialing (Telephony)

Initiate an outbound telephony call from the agent.

```javascript
await webex.cc.startOutdial('<E164_OR_VALID_NUMBER>'); // E164 is an International Standard of Telephone numbers
```

#### Request Parameters

| key | type | required | description |
| --- | --- | --- | --- |
| `destination` | string | yes | Phone number to dial (prefer E.164). |

#### Response Payload

- Resolves with a [TaskResponse](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-tasks#taskresponse) (includes identifiers like `interactionId`).

Ensure the agent is allowed to outdial and in the correct state.
