---
type: Excerpt
canonical_url: https://developer.webex.com/blog/meet-webex-node-webex-javascript-sdk-built-for-node-js
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- One SDK Family, Two Runtime-Focused Packages
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/blog/meet-webex-node-webex-javascript-sdk-built-for-node-js). [Full Markdown](../../../../blog/meet-webex-node-webex-javascript-sdk-built-for-node-js.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The [`webex-node`](https://www.npmjs.com/package/webex-node) package gives server-side JavaScript a supported Webex SDK entry point for Messaging, automation, bots, command-line tools, and backend services without loading browser-only media components.

---

## Selected section

## One SDK Family, Two Runtime-Focused Packages

Both packages come from the same [`webex-js-sdk`](https://github.com/webex/webex-js-sdk) project and share the same core concepts. In either environment, developers initialize a Webex client and work with APIs such as rooms, messages, memberships, people, teams, and webhooks.

The important difference is what each package loads and where it is intended to run.

| Choose | When your application runs in | Best suited for |
| --- | --- | --- |
| `webex-node` | Node.js, without a browser DOM | CLI tools, scheduled jobs, automation, bots, webhook services, and backend integrations using Messaging and related REST-backed APIs |
| `webex` | A web browser or browser-bundled application | Interactive web experiences, especially those using Meetings, Calling, Contact Center, or other browser media capabilities |

The full `webex` package includes media-oriented dependencies for Meetings, Calling, and Contact Center. Those capabilities rely on browser facilities and are intentionally excluded from `webex-node`. The result is not a second, unrelated SDK. It is a Node-focused distribution of the same SDK family with a runtime-appropriate capability boundary.

That boundary is also the principal limitation to remember: `webex-node` cannot be used for Meetings, Calling, or Contact Center media flows. If an application needs to join a meeting, place a call, or handle media in the browser, use `webex` and the appropriate browser SDK documentation.
