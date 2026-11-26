---
type: Excerpt
canonical_url: https://developer.webex.com/docs/widgets-callcontrolcad-participant-drop-widgets-beta
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Troubleshooting and feedback
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/widgets-callcontrolcad-participant-drop-widgets-beta). [Full Markdown](../../../../docs/widgets-callcontrolcad-participant-drop-widgets-beta.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Use the existing CallControlCAD widget to remove an eligible participant from an active conference. The Participants menu shows who is on the call, while the current primary agent can use Drop where permitted. This beta guide covers both the React widget and its Web Component wrapper.

## Selected section

## Troubleshooting and feedback

- **Drop is absent or disabled:** Check the current owner, call membership, consult state, and whether the target has joined. Customer-only calls do not show the conference roster; Supervisor rows are view-only.
- **Names or confirmation are missing:** Confirm the Widgets and Momentum Design component versions supplied for this beta are installed together. If a dialog fails to open, capture the sanitized browser error and version list; do not repeatedly click Drop.
- **Primary status or a dropped call looks stale:** Record which agent saw the issue, the event names and approximate timestamps, and whether a refresh changed the result. Avoid sharing raw routing payloads.
- **Drop fails:** The generic message does not identify the server-side reason. Check authorized backend diagnostics through your normal support process.

When reporting a result, send the scenario, React or Web Component integration mode, package versions, browser/OS, participant type, primary/secondary role, call direction, consult state, expected versus actual behavior, and sanitized console stack or routing event names/timestamps. **Do not send access tokens, names, phone numbers, ANI/DNIS, headers, request URLs, or raw event payloads.**
