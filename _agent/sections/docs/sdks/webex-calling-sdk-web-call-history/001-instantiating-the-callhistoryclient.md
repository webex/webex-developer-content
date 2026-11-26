---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-web-call-history
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Instantiating the CallHistoryClient
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-call-history). [Full Markdown](../../../../../docs/sdks/webex-calling-sdk-web-call-history.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article explains the call history feature available in the calling SDK. 

---

The calling SDK consists of various modules which are created at the time of its initialization — `CallHistoryClient` is one of those modules designed to facilitate the retrieving, managing, and interacting with `callHistory` records.

Refer to the [Getting Started documentation](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-quickstart) to understand how a `calling` instance is created and different modules are instantiated.

## Selected section

## Instantiating the CallHistoryClient

The `CallHistoryClient` is implemented as the `CallHistory` class in the SDK and there are two ways of instantiating it.

To instantiate just the `CallHistoryClient`, use the `createCallHistoryClient` method:

```javascript
const callHistory = createCallHistoryClient(webex, logger);
```

If the `CallHistoryClient` is initialized through the `calling` instantiation:

```javascript
const callHistory = calling.callHistory;
```
