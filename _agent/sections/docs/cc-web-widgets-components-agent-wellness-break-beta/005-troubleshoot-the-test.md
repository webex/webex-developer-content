---
type: Excerpt
canonical_url: https://developer.webex.com/docs/cc-web-widgets-components-agent-wellness-break-beta
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Troubleshoot the test
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/cc-web-widgets-components-agent-wellness-break-beta). [Full Markdown](../../../../docs/cc-web-widgets-components-agent-wellness-break-beta.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Use this guide to test Agent Wellness Break in the Cisco AI Assistant React widget. The widget shows suggestions and offers, runs the timed break after active work is complete, and returns the agent to Available.

## Selected section

## Troubleshoot the test

- **No suggestion or offer appears:** Check the organization settings, package versions, Station Login, effective wellness enablement, and AI Assistant real-time connection. The widget needs a live backend event.
- **A suggestion is hidden:** Check whether active Real Time Assist content has priority in the assistant panel.
- **The offer appears in an unexpected place:** Check whether the panel is open, closed, or minimized. Set `wellnessBreakOverlayTarget` for the host layout you use.
- **The break has not started:** Check for an active task or required wrap-up. The timer starts only after the agent enters the wellness state and work is safe.
- **The overlay does not cover the full app:** Check the target element and any iframe boundary. A child iframe cannot cover its parent page by itself.
- **The UI looks incomplete:** Check that the application uses `@momentum-ui/react-collaboration` 26.201.9 and the package peer dependencies.
