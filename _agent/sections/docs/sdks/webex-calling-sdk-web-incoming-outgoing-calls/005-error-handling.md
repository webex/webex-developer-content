---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-web-incoming-outgoing-calls
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Error Handling
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-incoming-outgoing-calls). [Full Markdown](../../../../../docs/sdks/webex-calling-sdk-web-incoming-outgoing-calls.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The `CallingClient` module in the Calling SDK provides inbound and outbound call functionality on registered lines.

---

A call instance is created for every call and then used to dial the call and listen for events. This document covers how the call instance is obtained and used in inbound/outbound calls.

## Selected section

## Error Handling

Calls will occasionally experience errors. An error event is triggered by the `call` object when an error is encountered. Listen for the `call_error` event to handle error scenarios.


```javascript
call.on('call_error', (callError: CallError) => {
  // Handle the error received for the ongoing call
    console.log('Error encountered on call with Id and description', 
      callError.getCallError().correlationId, callError.getCallError().message);
});
```

The `CallError` object contains the following members:

- `message` - Description of the call error.
- `type` - Type of error. This error can be either a call control error or a media error.
- `correlationId` - Correlation ID of the call that faced the issue.
