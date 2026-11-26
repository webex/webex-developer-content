---
type: Excerpt
canonical_url: https://developer.webex.com/blog/meet-webex-node-webex-javascript-sdk-built-for-node-js
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- A Clearer Path for Server-Side JavaScript
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/blog/meet-webex-node-webex-javascript-sdk-built-for-node-js). [Full Markdown](../../../../blog/meet-webex-node-webex-javascript-sdk-built-for-node-js.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The [`webex-node`](https://www.npmjs.com/package/webex-node) package gives server-side JavaScript a supported Webex SDK entry point for Messaging, automation, bots, command-line tools, and backend services without loading browser-only media components.

---

## Selected section

## A Clearer Path for Server-Side JavaScript

`webex-node` does not introduce a separate set of Webex APIs. Its most important capability is simpler and more practical: it gives server-side JavaScript a supported package boundary that matches the Node.js runtime.

For developers building terminal tools, automation, bots, and backend services, that means no browser shim, no accidental dependency on `window`, and no need to load media capabilities the application will never use. Install the package, initialize the familiar Webex client, and put Webex Messaging to work wherever Node.js runs.

To get started, visit the [Webex Node.js SDK documentation](https://developer.webex.com/messaging/docs/sdks/node) or explore the [`webex-node` source and README](https://github.com/webex/webex-js-sdk/tree/next/packages/webex-node).
