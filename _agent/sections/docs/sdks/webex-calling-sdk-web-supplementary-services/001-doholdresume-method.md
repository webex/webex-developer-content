---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-web-supplementary-services
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- doHoldResume Method
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

## doHoldResume Method

The `doHoldResume()` method puts the call on hold or resumes based on the current state of the call. If the call is connected, it's put on hold. Likewise if the call is already on hold, `doHoldResume()` resumes the call.



|            |      |
| ---------- | ---- |
| Parameters | --   |
| Returns    | void |

```javascript
// Assuming the call(inbound/outbound) is already established and we have the call instance.

call.doHoldResume(); // call is put on hold

call.doHoldResume(); // call is resumed
```

You'll want to create a listener for the `held` event on the `Call` object to monitor the hold status of the call:

```javascript
call.on('held', (callId: CallId) => {
  // Add code to handle successful hold
});
```

If the hold action is not successful, the `Call` object emits a `hold_error` event:

```javascript
call.on('hold_error', (error: CallError) => {
  // Add code to handle hold error
});
```

If a call is resumed from hold successfully, the `Call` object emits a `resumed` event:

```javascript
call.on('resumed', (callId: CallId) => {
  // Add code to handle successful resume
});
```

if the call is not resumed successfully, the `Call` object emits a `resume_error`:

```javascript
call.on('resume_error', (error: CallError) => {
  // Add code to handle resume error
});
```
