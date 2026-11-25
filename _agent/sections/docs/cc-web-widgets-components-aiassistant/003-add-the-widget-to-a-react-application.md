---
type: Excerpt
canonical_url: https://developer.webex.com/docs/cc-web-widgets-components-aiassistant
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Add the widget to a React application
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/cc-web-widgets-components-aiassistant). [Full Markdown](../../../../docs/cc-web-widgets-components-aiassistant.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Real Time Assist is a Cisco AI Assistant feature for Webex Contact Center. During an eligible live voice interaction, it uses the conversation context to identify customer intent and surface relevant suggested responses in the AI Assistant panel. Agents can review, copy, and rate suggestions without leaving the interaction. Use this guide to verify the beta in the sample application, then add either the React component or web component to your application.

## Selected section

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
