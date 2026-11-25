---
type: Excerpt
canonical_url: https://developer.webex.com/docs/cc-web-widgets-components-ai-summaries
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Set up the host application
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/cc-web-widgets-components-ai-summaries). [Full Markdown](../../../../docs/cc-web-widgets-components-ai-summaries.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Add AI-generated summaries to a Webex Contact Center Widgets application so agents can share conversation context during consults and transfers and review completed interactions during wrap-up.

## Selected section

## Set up the host application

Before installing the Beta:

- Complete the [Widgets Quickstart](https://developer.webex.com/docs/cc-web-widgets-quickstart) for the supported React setup, styling, peer dependencies, authentication, and station login. Replace its example Widgets version with the pinned version below.
- Have an administrator enable AI Assistant access and the required summary features for the applicable queues. See [Enable AI Assistant features in Control Hub for Webex Contact Center](https://help.webex.com/article/n9lk3t6/Enable-Cisco-AI-Assistant-for-Contact-Center) for licensing, user-profile, and recording prerequisites. Your host application provides the widget layout; Agent Desktop layout instructions apply to Agent Desktop.
- Check the **Supported languages for Summaries** table in [Multi-language Support for AI Assistant Features](https://help.webex.com/article/nlm6pob/Multi-language-Support-for-AI-Assistant-Features). Availability depends on the feature, locale, and tenant configuration.

Install with npm or Yarn:

```bash
npm install @webex/cc-widgets@1.28.0-next.66
# Alternative
yarn add @webex/cc-widgets@1.28.0-next.66
```

### Initialize and mount the widgets

1. Initialize the shared store with `store.init({webexConfig, access_token})` and await completion. If using `store.init({webex})` with an existing Webex instance, wait for that instance's `ready` event before initializing the store.
2. Mount **CallControlCAD** for the call-control and wrap-up experience, and **AIAssistant** for received summaries. Use the same initialized store for both, along with the station-login and task controls your application requires.
3. Complete station login, set the agent to Available, and verify that incoming calls and normal call controls work.

No separate AI-summary initialization flag is required. Received summaries in Cisco AI Assistant are available independently of Real-time Assist enablement.

### Check feature availability

Each summary type requires both its organization configuration and the interaction-specific task capability:

| Summary | Organization flag | Task capability |
| --- | --- | --- |
| Mid-call | `generatedSummaries.consultTransferSummariesEnabled === true` | `midCallEnabled === true` |
| Post-call | `generatedSummaries.wrapUpSummariesEnabled === true` | `postCallEnabled === true` |

The store and SDK use these values to control availability. A missing or false SDK gate disables the corresponding request. Use the station and destination combinations supported by the underlying call flow and tenant configuration.
