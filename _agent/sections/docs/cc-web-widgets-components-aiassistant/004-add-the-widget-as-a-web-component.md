---
type: Excerpt
canonical_url: https://developer.webex.com/docs/cc-web-widgets-components-aiassistant
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Add the widget as a web component
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/cc-web-widgets-components-aiassistant). [Full Markdown](../../../../docs/cc-web-widgets-components-aiassistant.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Real Time Assist is a Cisco AI Assistant feature for Webex Contact Center. During an eligible live voice interaction, it uses the conversation context to identify customer intent and surface relevant suggested responses in the AI Assistant panel. Agents can review, copy, and rate suggestions without leaving the interaction. Use this guide to verify the beta in the sample application, then add either the React component or web component to your application.

## Selected section

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
