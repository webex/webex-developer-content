---
type: Excerpt
canonical_url: https://developer.webex.com/docs/flow-orchestration
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Next steps
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/flow-orchestration). [Full Markdown](../../../../docs/flow-orchestration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md) [Restrictions](008-restrictions.md)

## Article introduction

Learn how to author a Webex Contact Center flow as a JSON document and import it through the Flow Orchestration APIs — entirely programmatically, without the UI.

## Selected section

## Next steps

- **Publish.** This guide stops at the validated draft. Publishing a draft (and the lock/unlock that goes with editing) is a separate step in the Flows API — see the Flow Orchestration API reference.
- **Expand the flow.** Discover more activities with `listActivityDefinitions`, resolve their inputs with `getActivityInputChoices`, and add them with `PATCH`. Routing activities (for example, queueing a contact) follow the same node/edge pattern shown here.
- **Automate authoring.** Because a flow is just a Flow JSON document validated by the `…:validate` endpoint, the discover → assemble → validate → import loop in this guide is the same foundation that AI-assisted flow authoring builds on.
