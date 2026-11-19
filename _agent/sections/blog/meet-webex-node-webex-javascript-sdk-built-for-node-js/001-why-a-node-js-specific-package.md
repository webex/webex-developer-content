---
type: Excerpt
canonical_url: https://developer.webex.com/blog/meet-webex-node-webex-javascript-sdk-built-for-node-js
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Why a Node.js-Specific Package?
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/blog/meet-webex-node-webex-javascript-sdk-built-for-node-js). [Full Markdown](../../../../blog/meet-webex-node-webex-javascript-sdk-built-for-node-js.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The [`webex-node`](https://www.npmjs.com/package/webex-node) package gives server-side JavaScript a supported Webex SDK entry point for Messaging, automation, bots, command-line tools, and backend services without loading browser-only media components.

---

## Selected section

## Why a Node.js-Specific Package?

For years, the [`webex`](https://www.npmjs.com/package/webex) npm package has given JavaScript developers a convenient way to add Webex capabilities to an application. It remains the right choice for browser experiences—including applications that use Webex Meetings, Calling, or Contact Center.

But a browser and a Node.js process are very different environments. A browser supplies APIs such as `window` and the media stack needed for real-time audio and video. A command-line script, automation worker, or backend service does not. Beginning with version 3 of the SDK, importing the full `webex` package directly into Node.js could load browser-dependent media components and fail with a `window is not defined` error.

That is the gap [`webex-node`](https://www.npmjs.com/package/webex-node) was created to fill.

Released in April 2025 and now documented on the [Webex for Developers Node.js SDK page](https://developer.webex.com/messaging/docs/sdks/node), `webex-node` provides a supported Webex JavaScript SDK entry point designed specifically for a Node.js runtime. It preserves the familiar SDK programming model for Messaging and related Webex APIs while leaving out browser-only media components.
