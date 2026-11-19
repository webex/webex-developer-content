---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/browser
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Upgrading
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/browser). [Full Markdown](../../../../../docs/sdks/browser.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Getting Started](003-getting-started.md) [Limitations](007-limitations.md)

## Article introduction

Add Webex products and features to your web apps with the Webex Browser SDK.

[GitHub](<https://github.com/webex/webex-js-sdk>)
[NPM](<https://www.npmjs.com/package/webex>)

## Selected section

## Upgrading

The `plugin-phone` plugin is deprecated and replaced with `plugin-meetings`. With this change comes significant code changes in upgrading to the meetings plugin. The meetings plugin is much more feature rich and maintained than the phone plugin.

For users of the phone plugin, one of the main changes from plugin-phone is the idea of having a meeting object that we are performing actions on. Instead of just "calling" a destination, a meeting object must be "created" and then "joined".

For more detailed information, please see the [upgrade guide](https://github.com/webex/webex-js-sdk/blob/master/packages/node_modules/%40webex/plugin-meetings/UPGRADING.md)
