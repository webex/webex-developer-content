---
type: Excerpt
canonical_url: https://developer.webex.com/docs/cc-web-widgets-components-aiassistant
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Validate the integration
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/cc-web-widgets-components-aiassistant). [Full Markdown](../../../../docs/cc-web-widgets-components-aiassistant.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Real Time Assist is a Cisco AI Assistant feature for Webex Contact Center. During an eligible live voice interaction, it uses the conversation context to identify customer intent and surface relevant suggested responses in the AI Assistant panel. Agents can review, copy, and rate suggestions without leaving the interaction. Use this guide to verify the beta in the sample application, then add either the React component or web component to your application.

## Selected section

## Validate the integration

Test the React component or web component during an active voice interaction and verify that:

- **Get Assistance** changes to the listening experience without an error.
- Suggested responses appear for the current interaction in chronological order.
- Adding context results in a subsequent response for the current interaction.
- Copy, like, and dislike controls respond without a UI error.
- Minimize, restore, full-screen, and close actions work with the host layout.
- `onRealTimeAssistReceived` runs for each new response when the callback is supplied.
- Ending the interaction clears its content, and a new interaction does not show content from the previous customer.
