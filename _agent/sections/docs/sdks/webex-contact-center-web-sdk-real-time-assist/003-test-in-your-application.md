---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-real-time-assist
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Test in your application
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-real-time-assist). [Full Markdown](../../../../../docs/sdks/webex-contact-center-web-sdk-real-time-assist.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Use this guide to test Real Time Assist with the Webex Contact Center SDK. Start with the sample application, then add the request, response, and feedback handling to your application.

## Selected section

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
