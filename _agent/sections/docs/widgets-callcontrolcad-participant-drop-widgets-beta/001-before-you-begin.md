---
type: Excerpt
canonical_url: https://developer.webex.com/docs/widgets-callcontrolcad-participant-drop-widgets-beta
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Before you begin
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/widgets-callcontrolcad-participant-drop-widgets-beta). [Full Markdown](../../../../docs/widgets-callcontrolcad-participant-drop-widgets-beta.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Use the existing CallControlCAD widget to remove an eligible participant from an active conference. The Participants menu shows who is on the call, while the current primary agent can use Drop where permitted. This beta guide covers both the React widget and its Web Component wrapper.

## Selected section

## Before you begin

Follow the [Contact Center Widgets quickstart](https://developer.webex.com/docs/cc-web-widgets-quickstart) to initialize the store, sign in, and render CallControlCAD. Use a beta-enabled Contact Center organization and compatible Widgets and Contact Center SDK builds supplied for your evaluation. Confirm the agent has an active voice conference and that your backend permits participant removal.

Participant Drop is part of **CallControlCAD** and `<widget-cc-call-control-cad>`. It adds no Drop-specific prop, Web Component attribute, or feature flag. The standard CallControl widget does not show this roster.
