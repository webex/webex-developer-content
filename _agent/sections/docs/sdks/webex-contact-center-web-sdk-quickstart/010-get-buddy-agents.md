---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-quickstart
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Get Buddy Agents
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-quickstart). [Full Markdown](../../../../../docs/sdks/webex-contact-center-web-sdk-quickstart.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Welcome to the Quick Start Guide for the Webex Contact Center (WxCC) SDK.

---

This guide is designed to help developers quickly set up, authenticate, and interact with the WxCC SDK. By following this guide and integrating the provided code snippets, you'll be able to log in an agent, manage agent states, and handle incoming tasks efficiently. Let's get started!

## Selected section

## Get Buddy Agents

To get the list of buddy agents in the given state and media according to agent profile settings:

```js
const buddyAgentsData = {
  state: 'Available', // Optional: Filter by agent state (e.g., 'Available', 'Idle')
  mediaType: 'telephony' // Optional: Filter by media type
};
const buddyAgentsResponse = await webex.cc.getBuddyAgents(buddyAgentsData);
// buddyAgentsResponse contains an array of buddy agents.
```
