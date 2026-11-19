---
type: Excerpt
canonical_url: https://developer.webex.com/docs/virtual-agent-transcripts-and-call-summary
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Prerequisites
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/virtual-agent-transcripts-and-call-summary). [Full Markdown](../../../../docs/virtual-agent-transcripts-and-call-summary.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

---

This document describes how a custom widget in the WxCC agent desktop, or a third-party custom desktop, can interact with the Serving API service. This interaction allows the retrieval of Virtual Agent transcripts and the Virtual Agent transfer summary when a call is transferred from a virtual agent to a human agent.

## Selected section

## Prerequisites

1. An access token with the `cjp:user` scope is required. See [Authentication](https://developer.webex.com/docs/authentication) for OAuth token generation.
2. The interaction ID of the current call is needed. For a custom widget in the WxCC Agent desktop, please refer [here](https://developer.webex.com/docs/desktop#javascript-sdk-and-modules). For third-party desktops, please refer [here](https://developer.webex.com/docs/contact-control-apis).

**Note:** The Interaction ID or Task ID is the same as the Conversation ID mentioned in this document.
