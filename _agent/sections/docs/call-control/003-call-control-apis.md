---
type: Excerpt
canonical_url: https://developer.webex.com/docs/call-control
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Call Control APIs
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/call-control). [Full Markdown](../../../../docs/call-control.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication and Authorization](002-authentication-and-authorization.md)

## Article introduction

Third-party services integrate with Webex Calling using admin-level APIs and admin-level tokens provided via Service Apps. This guide covers authentication, call control APIs, discovery APIs, telephony webhooks, and interest registration.

## Selected section

## Call Control APIs

Admin-level call control APIs allow a Service App to retrieve information about active calls and perform actions on them.

The admin-level call control APIs are derived from user-level call control APIs, but with an added `member` URL parameter. A member can be a Person, Workspace, or Virtual Line.

For more information, see the [Call Controls Members API](https://developer.webex.com/docs/api/v1/call-controls-members) documentation.
