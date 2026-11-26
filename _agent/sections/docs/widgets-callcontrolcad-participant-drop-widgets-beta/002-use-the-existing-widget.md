---
type: Excerpt
canonical_url: https://developer.webex.com/docs/widgets-callcontrolcad-participant-drop-widgets-beta
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Use the existing widget
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/widgets-callcontrolcad-participant-drop-widgets-beta). [Full Markdown](../../../../docs/widgets-callcontrolcad-participant-drop-widgets-beta.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Use the existing CallControlCAD widget to remove an eligible participant from an active conference. The Participants menu shows who is on the call, while the current primary agent can use Drop where permitted. This beta guide covers both the React widget and its Web Component wrapper.

## Selected section

## Use the existing widget

In a React integration, render the existing component after your normal store and agent setup:

```tsx
import {CallControlCAD} from '@webex/cc-widgets';

<CallControlCAD />;
```

For a Web Component integration, register the components through the existing package entry point, initialize the store as described in the [Widgets quickstart](https://developer.webex.com/docs/cc-web-widgets-quickstart), and render the existing element:

```ts
import {store} from '@webex/cc-widgets/wc';

// Complete your normal store.init(...) and agent sign-in before rendering.
const callControl = document.createElement('widget-cc-call-control-cad');
document.body.appendChild(callControl);
```

No Participant Drop switch is needed. See the [CallControlCAD component guide](https://developer.webex.com/docs/cc-web-widgets-components-callcontrolcad) for general integration details.

In the React sample, select **Call Controls with Call Associated Data (CAD)** before initializing the widgets.

![React Widgets sample with Call Controls with Call Associated Data (CAD) selected in the widget list.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt32019217202a0258/6ac3841f517fb6cd17971e03/participant-drop-widgets-cad-setup.png)

*React sample setup. The selected CAD widget provides the participant menu shown below.*
