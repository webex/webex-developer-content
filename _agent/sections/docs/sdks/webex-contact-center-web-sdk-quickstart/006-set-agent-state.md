---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-quickstart
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Set Agent State
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-quickstart). [Full Markdown](../../../../../docs/sdks/webex-contact-center-web-sdk-quickstart.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Welcome to the Quick Start Guide for the Webex Contact Center (WxCC) SDK.

---

This guide is designed to help developers quickly set up, authenticate, and interact with the WxCC SDK. By following this guide and integrating the provided code snippets, you'll be able to log in an agent, manage agent states, and handle incoming tasks efficiently. Let's get started!

## Selected section

## Set Agent State

Agents can change their status using `setAgentState`:

```js
const agentStateResponse = await webex.cc.setAgentState({
  state: 'Available', // or 'Idle'
  auxCodeId: `<AUX_CODE_ID>`, // Required if state is 'Idle'
  lastStateChangeReason: `<REASON>`,
  // agentId: `<AGENT_ID>` // Typically not needed, SDK infers from context
});
```

To listen for agent state changes from other sources:

```js
webex.cc.on('agent:stateChange', (data) => {
  console.log('Agent state changed:', data);
});
```
