---
type: Excerpt
canonical_url: https://developer.webex.com/docs/cc-web-widgets-components-agent-wellness-break-beta
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Validate the integration
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/cc-web-widgets-components-agent-wellness-break-beta). [Full Markdown](../../../../docs/cc-web-widgets-components-agent-wellness-break-beta.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Use this guide to test Agent Wellness Break in the Cisco AI Assistant React widget. The widget shows suggestions and offers, runs the timed break after active work is complete, and returns the agent to Available.

## Selected section

## Validate the integration

- Before a live suggestion or offer arrives, the widget shows no wellness action. A consumed suggestion is not reused.
- An open assistant shows one offer card. A closed or minimized assistant shows one actionable notification.
- A direct offer changes the agent to `WellbeingBreak` before it sends `ACCEPTED`. **Later** sends `REJECTED`; an unanswered offer sends `NO_RESPONSE` once.
- An approved manual request starts the break without a second `ACCEPTED` action.
- Active tasks and required wrap-up finish before the timed break starts. Completion returns the agent to Available with aux code `0`.
- The overlay traps focus during the break, Escape does not dismiss it, and focus returns after completion. Reduced motion uses a static treatment.
- A media failure does not block Available restoration. Logout, session changes, and unmount stop work for the old session.
