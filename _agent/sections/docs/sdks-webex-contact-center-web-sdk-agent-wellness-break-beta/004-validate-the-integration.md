---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks-webex-contact-center-web-sdk-agent-wellness-break-beta
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Validate the integration
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks-webex-contact-center-web-sdk-agent-wellness-break-beta). [Full Markdown](../../../../docs/sdks-webex-contact-center-web-sdk-agent-wellness-break-beta.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Use this guide to test Agent Wellness Break with the Webex Contact Center SDK. The SDK delivers wellness events and actions. Your application presents the break, waits for active work to finish, and returns the agent to Available.

## Selected section

## Validate the integration

- A suggestion enables one manual request. HTTP acceptance leaves the UI pending until a later approval or denial event, or until the five-minute decision timeout.
- A fresh suggestion clears an earlier pending request and its timer and enables a new request.
- A denial clears pending state and disables the request action, even if no request is pending.
- A missing decision clears pending UI after five minutes. A later direct offer follows the direct-offer path and sends the appropriate response.
- A pending request approved by `PROVIDE_WELLNESS_BREAK` starts the state-change flow without a second `ACCEPTED` action.
- A direct offer sends one of `ACCEPTED`, `REJECTED`, or `NO_RESPONSE`. Acceptance follows a successful state-change request.
- Active work and wrap-up finish before the break timer starts. Completion returns the agent to Available with aux code `0`.
- Logout or a station-session change clears pending UI and its timer, and prevents late results or recovery from acting on a later session.
