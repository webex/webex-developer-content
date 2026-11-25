---
type: Excerpt
canonical_url: https://developer.webex.com/docs/cc-web-widgets-components-aiassistant
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Test with the Widgets sample application
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/cc-web-widgets-components-aiassistant). [Full Markdown](../../../../docs/cc-web-widgets-components-aiassistant.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Real Time Assist is a Cisco AI Assistant feature for Webex Contact Center. During an eligible live voice interaction, it uses the conversation context to identify customer intent and surface relevant suggested responses in the AI Assistant panel. Agents can review, copy, and rate suggestions without leaving the interaction. Use this guide to verify the beta in the sample application, then add either the React component or web component to your application.

## Selected section

## Test with the Widgets sample application

Run this test first. If it fails, fix the organization, agent, or knowledge-base setup before changing your application.

1. Sign in to the [Webex Developer Portal](https://developer.webex.com/) as the test agent. Open the user menu and copy the developer access token.
1. Open the [Webex Contact Center Widgets sample application](https://widgets.webex.com/samples-cc-react-app/index.html).
1. Paste the developer access token, initialize the widgets, and select **AI Assistant** in **Select Widgets to Show**.

    ![Webex Contact Center Widgets sample application with AI Assistant selected in the list of widgets to show.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt4723244b4adbf796/6a7b5abaf6825746c0590839/real-time-assist-widgets-selection.png)

1. Use the Station Login widget to sign in, and then change the agent state to **Available**.
1. Open Cisco AI Assistant before an eligible interaction is active. Confirm that the landing experience appears and that no suggested response is displayed.

    ![Cisco AI Assistant landing experience showing Real-time Assist, Wellness breaks, and Smart summaries before an interaction starts.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt72f8edbf7c125a8f/6a7b5ad542a117328c953656/real-time-assist-landing-experience.png)

1. Start and accept an incoming voice interaction. Keep the interaction active while you test several responses.
1. Open Cisco AI Assistant during the active interaction. Confirm that **Get Assistance** appears.

    ![Cisco AI Assistant panel for an active voice interaction with the Get Assistance button ready to select.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt2278aaedb69da3c5/6a7b5adc448e4ecfb05b81a9/real-time-assist-get-assistance.png)

    Select **Get Assistance**. Confirm that the request shows progress and the panel changes to the **Listening** state.

    ![Cisco AI Assistant panel in Listening mode during an active customer interaction.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt41ed33a261dd1fa1/6a7c9b5ede2315e900fd236b/real-time-assist-listening-mode.jpg)

1. Continue the interaction until one or more suggested response cards appear. Confirm that the cards are ordered chronologically and contain understandable, relevant responses for the current interaction.
1. Use **Add context** to provide information for the next response, submit the context, and continue the interaction.
1. Select copy, like, and dislike on a response. Confirm that each control responds without a UI error.
1. Minimize and restore the panel, toggle full-screen mode, and close the panel. Confirm that the panel remains usable and that the host layout responds correctly.
1. End the interaction. Start a different interaction, if available, and confirm that content from the previous customer is not displayed in the new session.

The setup is ready when the widget receives responses for the active interaction, all three response actions work, and content from one interaction does not appear in the next.
