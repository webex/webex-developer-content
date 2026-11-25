---
type: Excerpt
canonical_url: https://developer.webex.com/docs/cc-web-widgets-components-agent-wellness-break-beta
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Before you begin
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/cc-web-widgets-components-agent-wellness-break-beta). [Full Markdown](../../../../docs/cc-web-widgets-components-agent-wellness-break-beta.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Use this guide to test Agent Wellness Break in the Cisco AI Assistant React widget. The widget shows suggestions and offers, runs the timed break after active work is complete, and returns the agent to Available.

## Selected section

## Before you begin

- Join the [Webex Developer Beta Program](https://developer.webex.com/docs/webex-developer-beta-program) and use an approved Contact Center organization and agent.
- Confirm that the organization has an AI Assistant entitlement and that agent wellbeing and wellness break reminders are enabled. The widget uses the effective SDK enablement flag; your application does not need a separate wellness feature toggle.
- Use `@webex/cc-widgets` **1.28.0-next.62** and `@webex/contact-center` **3.12.0-next.133**. Use the `webex` aggregate package **3.12.0-next.220** if your application uses it. Pin these package versions for this beta.
- Use `@momentum-ui/react-collaboration` **26.201.9**. The published Station Login package requires this version. Install the other peer dependencies required by your widget package, including compatible React, React DOM, and `@momentum-ui/web-components` versions.
- Complete the [Webex Contact Center Web Widgets Quickstart](https://developer.webex.com/docs/cc-web-widgets-quickstart). Initialize the shared store once and complete Station Login before testing.
- Use a React host with enough space for the break overlay. An iframe can cover only its own viewport unless its parent supplies an overlay.

Watch the [Widgets wellness demonstration](https://app.vidcast.io/share/c557c146-0941-41a4-ac92-493297d5da83) for an example of the test flow.
