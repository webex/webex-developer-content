---
type: Excerpt
canonical_url: https://developer.webex.com/docs/cc-web-widgets-components-aiassistant
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Troubleshoot the test
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/cc-web-widgets-components-aiassistant). [Full Markdown](../../../../docs/cc-web-widgets-components-aiassistant.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Real Time Assist is a Cisco AI Assistant feature for Webex Contact Center. During an eligible live voice interaction, it uses the conversation context to identify customer intent and surface relevant suggested responses in the AI Assistant panel. Agents can review, copy, and rate suggestions without leaving the interaction. Use this guide to verify the beta in the sample application, then add either the React component or web component to your application.

## Selected section

## Troubleshoot the test

- **`AIAssistant` is missing from the package:** Confirm that your dependency version includes the component, then reinstall dependencies.
- **The widget says the feature is unavailable:** Confirm the organization's AI Assistant entitlement and verify that Real Time Assist is enabled for the agent.
- **The panel opens but no responses arrive:** Confirm that the shared store contains the current agent and active voice task. Then repeat the sample-application test to separate configuration problems from host-application problems.
- **Full-screen mode does not change the layout:** Handle `onFullScreenToggle` and apply the full-screen layout in the host application.
- **A previous customer's content appears:** Confirm that the host does not retain or restore widget state from the completed interaction.
