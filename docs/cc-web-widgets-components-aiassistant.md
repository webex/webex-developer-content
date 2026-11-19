---
type: Guide
title: Webex Contact Center Web Widgets | Components | AI Assistant
display_title: Overview
canonical_url: https://developer.webex.com/docs/cc-web-widgets-components-aiassistant
content_type: documentation
product_group:
- webex-suite
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/cc-web-widgets-components-aiassistant)

Real Time Assist is a Cisco AI Assistant feature for Webex Contact Center. During an eligible live voice interaction, it uses the conversation context to identify customer intent and surface relevant suggested responses in the AI Assistant panel. Agents can review, copy, and rate suggestions without leaving the interaction. Use this guide to verify the beta in the sample application, then add either the React component or web component to your application.

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

## Add the widget to a React application

Import the AI Assistant widget. Your application should already initialize the shared Contact Center store as described in the Quickstart; do not initialize a second store for this widget.

```js
import {AIAssistant} from '@webex/cc-widgets';
```

The widget reads the current agent, task, feature configuration, and Real Time Assist responses from the shared store. It also sends the request and feedback actions; your host application does not need to call the Real Time Assist SDK methods separately.

Add the widget to your component. All callbacks are optional; use the ones your host application needs.

```jsx
import {useState} from 'react';
import {AIAssistant} from '@webex/cc-widgets';

const [isAIAssistantFullScreen, setIsAIAssistantFullScreen] = useState(false);

<AIAssistant
  className={isAIAssistantFullScreen ? 'ai-assistant--host-full' : undefined}
  onOpen={() => console.log('AI Assistant opened')}
  onMinimize={() => console.log('AI Assistant minimized')}
  onRestore={() => console.log('AI Assistant restored')}
  onClose={() => setIsAIAssistantFullScreen(false)}
  onFullScreenToggle={(isFullScreen) => setIsAIAssistantFullScreen(isFullScreen)}
  onRealTimeAssistReceived={(payload) => console.log('Real Time Assist response', payload)}
/>
```

`onRealTimeAssistReceived` is an optional notification callback. The widget renders the response itself; use the callback only when your host application needs to log or react to a new response.

The widget reports full-screen changes through `onFullScreenToggle`, but it does not resize the host layout. Your application must apply the corresponding layout or CSS.

## Add the widget as a web component

To use the AI Assistant widget without rendering it as a React component, import the web-component entry point. This registers the `widget-cc-ai-assistant` custom element and exports the same shared store used by the React components.

```js
import {store} from '@webex/cc-widgets/wc';

await store.init({
  webexConfig,
  access_token: accessToken,
});

const aiAssistant = document.createElement('widget-cc-ai-assistant');

aiAssistant.onOpen = () => console.log('AI Assistant opened');
aiAssistant.onFullScreenToggle = (isFullScreen) => {
  console.log('AI Assistant full-screen state:', isFullScreen);
};
aiAssistant.onRealTimeAssistReceived = (payload) => {
  console.log('Real Time Assist response:', payload);
};

document.body.appendChild(aiAssistant);
```

Use the `webexConfig` and `accessToken` values from the Quickstart. If another Contact Center widget has already initialized `store`, do not call `store.init()` again. Complete station login before testing the custom element.

## Validate the integration

Test the React component or web component during an active voice interaction and verify that:

- **Get Assistance** changes to the listening experience without an error.
- Suggested responses appear for the current interaction in chronological order.
- Adding context results in a subsequent response for the current interaction.
- Copy, like, and dislike controls respond without a UI error.
- Minimize, restore, full-screen, and close actions work with the host layout.
- `onRealTimeAssistReceived` runs for each new response when the callback is supplied.
- Ending the interaction clears its content, and a new interaction does not show content from the previous customer.

## Troubleshoot the test

- **`AIAssistant` is missing from the package:** Confirm that your dependency version includes the component, then reinstall dependencies.
- **The widget says the feature is unavailable:** Confirm the organization's AI Assistant entitlement and verify that Real Time Assist is enabled for the agent.
- **The panel opens but no responses arrive:** Confirm that the shared store contains the current agent and active voice task. Then repeat the sample-application test to separate configuration problems from host-application problems.
- **Full-screen mode does not change the layout:** Handle `onFullScreenToggle` and apply the full-screen layout in the host application.
- **A previous customer's content appears:** Confirm that the host does not retain or restore widget state from the completed interaction.
