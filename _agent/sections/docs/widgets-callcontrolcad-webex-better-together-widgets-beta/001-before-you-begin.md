---
type: Excerpt
canonical_url: https://developer.webex.com/docs/widgets-callcontrolcad-webex-better-together-widgets-beta
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Before you begin
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/widgets-callcontrolcad-webex-better-together-widgets-beta). [Full Markdown](../../../../docs/widgets-callcontrolcad-webex-better-together-widgets-beta.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Release scope and limitations](006-release-scope-and-limitations.md)

## Article introduction

Use this guide to test Webex Better Together with the Webex Contact Center Widgets package. Agents can handle supported voice-call actions from an embedded host application while the call runs in Webex App on the same computer.

## Selected section

## Before you begin

- Complete the [Webex Contact Center Web Widgets Quickstart](https://developer.webex.com/docs/cc-web-widgets-quickstart), including widget initialization, authentication, and station login.
- Use a Contact Center organization provisioned for Webex Together / wxApp telephony.
- Sign in using an **Extension** or **Agent DN** station login. Browser/WebRTC-only login is not the supported answer path.
- Run Webex App desktop version 44.12 or later on the same computer as the embedded application and sign in as the same user.
- Use React 18.3.1 or later for a React host.
- Join the [Webex Developer Beta Program](https://developer.webex.com/docs/webex-developer-beta-program) and use the beta feedback channel shared with your invitation.

The Contact Center SDK handles Webex App telephony routing and mute synchronization. The widgets are the UI layer; no new widget export is required. This release uses the existing `IncomingTask`, `TaskList`, and `CallControl` widgets.
