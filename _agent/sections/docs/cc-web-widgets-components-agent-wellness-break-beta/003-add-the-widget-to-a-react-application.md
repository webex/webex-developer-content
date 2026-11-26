---
type: Excerpt
canonical_url: https://developer.webex.com/docs/cc-web-widgets-components-agent-wellness-break-beta
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Add the widget to a React application
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/cc-web-widgets-components-agent-wellness-break-beta). [Full Markdown](../../../../docs/cc-web-widgets-components-agent-wellness-break-beta.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Use this guide to test Agent Wellness Break in the Cisco AI Assistant React widget. The widget shows suggestions and offers, runs the timed break after active work is complete, and returns the agent to Available.

## Selected section

## Add the widget to a React application

Keep the shared store and Station Login flow from the Widgets quickstart. Import `AIAssistant` from the existing `@webex/cc-widgets` aggregate. Your application does not need to call the wellness SDK methods when it uses this widget.

```jsx
import {AIAssistant} from '@webex/cc-widgets';

<AIAssistant
  wellnessBreakOverlayTarget="viewport"
  onWellnessBreakOffered={() => recordLifecycle('offered')}
  onWellnessBreakAccepted={() => recordLifecycle('accepted')}
  onWellnessBreakStarted={() => recordLifecycle('started')}
  onWellnessBreakEnded={() => recordLifecycle('ended')}
  onWellnessBreakError={(error) => recordErrorCode(error.code)}
/>
```

The callbacks are optional. `recordLifecycle()` and `recordErrorCode()` represent your application's handlers. Do not record notification text, agent identifiers, or customer data.

`wellnessBreakOverlayTarget` defaults to `"viewport"`. Use `"assistant"` to cover the assistant root, or pass an `HTMLElement` for a custom React host container. The active overlay stays in place if the assistant panel is closed or minimized. If the widget is inside an iframe, viewport coverage stops at the iframe boundary.

The widget supplies its wellness animation and audio. It loads the media when the break needs it. If audio cannot play or animation cannot load, the break continues with a silent or static presentation. You can set `wellnessAudioUrl` if your application uses an approved audio URL.
