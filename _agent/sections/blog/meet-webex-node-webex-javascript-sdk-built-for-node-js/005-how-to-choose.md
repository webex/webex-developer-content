---
type: Excerpt
canonical_url: https://developer.webex.com/blog/meet-webex-node-webex-javascript-sdk-built-for-node-js
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- How to Choose
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/blog/meet-webex-node-webex-javascript-sdk-built-for-node-js). [Full Markdown](../../../../blog/meet-webex-node-webex-javascript-sdk-built-for-node-js.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The [`webex-node`](https://www.npmjs.com/package/webex-node) package gives server-side JavaScript a supported Webex SDK entry point for Messaging, automation, bots, command-line tools, and backend services without loading browser-only media components.

---

## Selected section

## How to Choose

The simplest decision rule is to choose by runtime and required capability:

- If the code runs as a Node.js process and needs Messaging or related management APIs, start with `webex-node`.
- If the code runs in a browser and needs a user-facing Webex experience, use `webex`.
- If the application needs Meetings, Calling, or Contact Center media flows, use `webex`; those capabilities are outside the scope of `webex-node`.
- If the solution has both a browser frontend and a Node.js backend, it can use both packages—each on its own side of the application boundary.

That last pattern is often the most useful. A browser can own the interactive experience and real-time media, while a backend safely performs scheduled work, responds to webhooks, and integrates Webex with other systems.
