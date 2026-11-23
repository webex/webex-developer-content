---
type: Excerpt
canonical_url: https://developer.webex.com/docs/cc-web-widgets-quickstart
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Known Issues/Limitations
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/cc-web-widgets-quickstart). [Full Markdown](../../../../docs/cc-web-widgets-quickstart.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](001-prerequisites.md)

## Article introduction

This Quickstart Guide walks you through integrating Webex Contact Center capabilities using React widgets into your application from the ground up. Follow these steps to create a fully functional application.

## Selected section

## Known Issues/Limitations

- Changing the versions of dependencies other than what is mentioned in the `package.json` file section above might break the application, so please use all the versions as specified in this guide.
- Error after transferring call: When you refresh the page while you have an incoming call, the `onAcceptCallback` on the `IncomingTask` widget is not invoked.
