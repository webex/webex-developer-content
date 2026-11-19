---
type: Guide
title: Webex Contact Center Web SDK | Real Time Assist
display_title: Real Time Assist
canonical_url: https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-real-time-assist
content_type: documentation
product_group:
- webex-contact-center
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-real-time-assist)

Use this guide to test Real Time Assist with the Webex Contact Center SDK. Start with the sample application, then add the request, response, and feedback handling to your application.

## Before you begin

Before testing, make sure that:

- The organization has an AI Assistant trial or paid entitlement (`AI-Assistant-SKY`).
- An administrator has enabled AI Assistant Real Time Assist for both the organization and the agent profile.
- The agent can register, complete station login, change to the **Available** state, and receive voice interactions.
- The administrator has configured the knowledge bases and skills that Real Time Assist uses. See [Configure Real Time Assist](https://help.webex.com/article/nztf84bb) and the configuration walkthrough below.
- Your application has completed the setup in the [Webex Contact Center Web SDK Quickstart](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-quickstart).

### Configure Real Time Assist

Watch the following walkthrough to configure Real Time Assist.

<iframe src="https://app.vidcast.io/share/embed/9dfb9a60-7fb2-4c07-a67f-7caf5e891b13" width="100%" height="582" title="Configure Real Time Assist" frameborder="0" loading="lazy" allowfullscreen></iframe>

If the embedded video does not load, [open the Real Time Assist configuration walkthrough in Vidcast](https://app.vidcast.io/share/9dfb9a60-7fb2-4c07-a67f-7caf5e891b13).

## Test with the SDK sample application

Run this test first. If it fails, fix the organization or agent setup before changing your application.

1. Open the [Webex Contact Center SDK sample application](https://webex.github.io/webex-js-sdk/samples/contact-center/).
1. Initialize the SDK with the test agent's access token.
1. Register the agent, complete station login, and change the agent state to **Available**.
1. Start and accept an incoming voice interaction.
1. Request Real Time Assist and confirm that a suggested response is received for the active interaction.
1. Add context and request another response.
1. Test the like, dislike, and copy actions on the response.

The setup is ready when the sample application receives responses for the active interaction and all three feedback actions complete without an error.

Watch the following demonstration of this flow.

<iframe src="https://app.vidcast.io/share/embed/6c256ddc-8947-4301-9ed6-52bfa25d2ef3" width="100%" height="582" title="Test Real Time Assist with the Webex Contact Center SDK sample application" frameborder="0" loading="lazy" allowfullscreen></iframe>

If the embedded video does not load, [open the SDK sample application demonstration in Vidcast](https://app.vidcast.io/share/6c256ddc-8947-4301-9ed6-52bfa25d2ef3).

## Test in your application

Real Time Assist is available from `webex.cc.apiAIAssistant`. The examples below assume that your application has initialized the SDK and that `task` is the active voice task received from `task:incoming`.

Complete these steps in order:

1. Attach the response listener to the task.
1. Accept the task.
1. Call the request API from your **Get Assistance** control.
1. Render the response and retain its `adaptiveCardId`.
1. Send the appropriate feedback action when the agent selects like, dislike, or copy.

### Receive suggested responses

Attach the `SUGGESTED_RESPONSE` listener before accepting the task. The handler receives a payload whose suggestion content is in its `data` property.

```js
webex.cc.on('task:incoming', async (task) => {
  task.on('SUGGESTED_RESPONSE', (payload) => {
    renderSuggestion(payload.data, {
      onLike: () =>
        reportResponseAction(task, payload.data.adaptiveCardId, 'likeButton'),
      onDislike: () =>
        reportResponseAction(task, payload.data.adaptiveCardId, 'dislikeButton'),
      onCopy: () =>
        reportResponseAction(task, payload.data.adaptiveCardId, 'copyButton'),
    });
  });

  await task.accept();

  // Connect requestAssistance(task) to your Get Assistance control.
});
```

`renderSuggestion()` and its action handlers represent your application's UI code. Adapt them to your framework, but keep each response's `adaptiveCardId` with that response. Do not reuse an ID from an earlier card or interaction.

If your application restores a task instead of receiving `task:incoming`, attach the same listener to the restored task before requesting assistance.

### Request assistance

Pass the agent and interaction identifiers for the active task. Connect this function to the control that the agent uses to request assistance.

```js
async function requestAssistance(task, context) {
  const request = {
    agentId: task.data.agentId,
    interactionId: task.data.interactionId,
    languageCode: 'en',
  };

  if (context?.trim()) {
    request.context = context.trim();
  }

  return webex.cc.apiAIAssistant.getRealTimeAssistance(request);
}
```

Request a response without extra context:

```js
await requestAssistance(task);
```

Or pass the text entered in your **Add context** field:

```js
await requestAssistance(
  task,
  'Customer wants a concise explanation of the refund policy.'
);
```

This example uses `en`. Use a language code supported by your Real Time Assist configuration.

### Report an agent action

When the agent likes, dislikes, or copies a response, call `sendRealTimeAssistanceUserAction()`. Pass the `adaptiveCardId` stored with that response and one of these action IDs:

- Like: `likeButton`
- Dislike: `dislikeButton`
- Copy: `copyButton`

```js
async function reportResponseAction(task, adaptiveCardId, actionId) {
  return webex.cc.apiAIAssistant.sendRealTimeAssistanceUserAction({
    agentId: task.data.agentId,
    interactionId: task.data.interactionId,
    adaptiveCardId,
    actionId,
  });
}
```

The response-listener example connects this function to the like, dislike, and copy controls.

## Validate the integration

Complete an active voice interaction and verify that:

- A request without extra context completes without an SDK error.
- The task receives a `SUGGESTED_RESPONSE` event and your application displays the response.
- A request with extra context returns a new response for the same interaction.
- Like, dislike, and copy actions complete without an SDK error and use the correct `adaptiveCardId`.
- Ending an interaction clears its responses from your UI, and a new interaction does not show content from the previous customer.

## Troubleshoot the test

- **The request returns a feature-disabled error:** Confirm that Real Time Assist is enabled for both the organization and the agent profile.
- **The request succeeds but no response event arrives:** Confirm that the listener is attached to the current task before the request and that the interaction is still active.
- **Feedback fails:** Confirm that the `interactionId` belongs to the current task and that `adaptiveCardId` came from the response whose control the agent selected.
- **A response appears under the wrong customer:** Clear your rendered responses when the task ends and keep response state separate for each interaction.
