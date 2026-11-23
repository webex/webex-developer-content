---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-web-supplementary-services
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- sendDigit Method
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-supplementary-services). [Full Markdown](../../../../../docs/sdks/webex-calling-sdk-web-supplementary-services.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article describes the Webex Calling SDK supplementary services such as hold, resume, blind transfer, and consult transfer.

---

Once an inbound or outbound call is in an established state, you can access a set of supplementary services. To access these services, you'll need the `Call` object, which is created when a call is initialized. Refer to [Inbound/Outbound Calls](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-incoming-outgoing-calls) for information on creating a `Call` object.

The Call object exposes the following supplementary service methods:

- `doHoldResume()`
- `completeTransfer()`
- `sendDigit()`

## Selected section

## sendDigit Method

The `sendDigit()` method sends a single DTMF digit on an established call which is useful, for instance, when navigating an Interactive Voice Response (IVR) system where a user is expected to enter a touch tone corresponding to menu item.

The method accepts a string representing the DTMF digit as a parameter:



|            |        |
| ---------- | ------ |
| Parameters | `string` |
| Returns    | `void`   |

```javascript
const call = line.makeCall();
call.sendDigit('1');
```
