---
type: Excerpt
canonical_url: https://developer.webex.com/docs/cc-web-widgets-components-aiassistant
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Before you begin
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/cc-web-widgets-components-aiassistant). [Full Markdown](../../../../docs/cc-web-widgets-components-aiassistant.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Real Time Assist is a Cisco AI Assistant feature for Webex Contact Center. During an eligible live voice interaction, it uses the conversation context to identify customer intent and surface relevant suggested responses in the AI Assistant panel. Agents can review, copy, and rate suggestions without leaving the interaction. Use this guide to verify the beta in the sample application, then add either the React component or web component to your application.

## Selected section

## Before you begin

Before testing, make sure that:

- The organization has an AI Assistant trial or paid entitlement.
- An administrator has enabled Real Time Assist for both the organization and the test agent.
- The agent can complete station login, change to the **Available** state, and receive voice interactions.
- The administrator has configured the knowledge bases and skills that Real Time Assist uses. See [Configure Real Time Assist](https://help.webex.com/article/nztf84bb) and the configuration walkthrough below.
- You have completed the [Webex Contact Center Web Widgets Quickstart](https://developer.webex.com/webex-contact-center/docs/cc-web-widgets-quickstart).

### Configure Real Time Assist

Watch the following walkthrough to configure Real Time Assist.

<iframe src="https://app.vidcast.io/share/embed/9dfb9a60-7fb2-4c07-a67f-7caf5e891b13" width="100%" height="582" title="Configure Real Time Assist" frameborder="0" loading="lazy" allowfullscreen></iframe>

If the embedded video does not load, [open the Real Time Assist configuration walkthrough in Vidcast](https://app.vidcast.io/share/9dfb9a60-7fb2-4c07-a67f-7caf5e891b13).

### Watch the widget demonstration

The following video shows Real Time Assist in the Cisco AI Assistant widget.

<iframe src="https://app.vidcast.io/share/embed/468e2e52-6e91-4728-968d-ee04bb95e983" width="100%" height="582" title="Real Time Assist in the Cisco AI Assistant widget" frameborder="0" loading="lazy" allowfullscreen></iframe>

If the embedded video does not load, [open the Real Time Assist widget demonstration in Vidcast](https://app.vidcast.io/share/468e2e52-6e91-4728-968d-ee04bb95e983).

Complete the sample test whether you plan to evaluate or integrate the feature. If you only want to evaluate it, stop after the sample test. For an integration, continue with either the React section or the web-component section. You do not need to implement both.
