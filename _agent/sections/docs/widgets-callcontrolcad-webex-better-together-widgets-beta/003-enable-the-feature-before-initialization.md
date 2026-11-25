---
type: Excerpt
canonical_url: https://developer.webex.com/docs/widgets-callcontrolcad-webex-better-together-widgets-beta
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Enable the feature before initialization
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/widgets-callcontrolcad-webex-better-together-widgets-beta). [Full Markdown](../../../../docs/widgets-callcontrolcad-webex-better-together-widgets-beta.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md) [Release scope and limitations](006-release-scope-and-limitations.md)

## Article introduction

Use this guide to test Webex Better Together with the Webex Contact Center Widgets package. Agents can handle supported voice-call actions from an embedded host application while the call runs in Webex App on the same computer.

## Selected section

## Enable the feature before initialization

Set `webexConfig.cc.enableWxBetterTogether` before calling `store.init()`. The setting defaults to `false` and is initialization-only in this release.

```js
import { store } from '@webex/cc-widgets';

const webexConfig = {
  cc: {
    enableWxBetterTogether: true,
  },
};

await store.init({ webexConfig, access_token: accessToken });
```

If your host initializes a Webex instance separately, set the same Contact Center configuration before initializing that instance and then initialize the widgets with it. The feature is not gated by a Contact Center user or organization feature toggle.
