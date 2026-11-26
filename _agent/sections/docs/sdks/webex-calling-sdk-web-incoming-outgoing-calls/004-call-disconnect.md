---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-web-incoming-outgoing-calls
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Call Disconnect
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-incoming-outgoing-calls). [Full Markdown](../../../../../docs/sdks/webex-calling-sdk-web-incoming-outgoing-calls.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The `CallingClient` module in the Calling SDK provides inbound and outbound call functionality on registered lines.

---

A call instance is created for every call and then used to dial the call and listen for events. This document covers how the call instance is obtained and used in inbound/outbound calls.

## Selected section

## Call Disconnect

Disconnect the call using the `call` object's `end()` method or listen for `disconnect` events coming from the other side.

Refer to the below examples:

1.  Listen for a `disconnect` event if the remote party disconnects the call.

    ```javascript
    call.on('disconnect', (correlationId: string) => {
      // Add action to clear out the call on the application
    });
    ```

2.  Once the disconnect event is received use the `call` object's `end()` method available to disconnect the call.

    ```javascript
    call.end();
    ```
