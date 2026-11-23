---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-quickstart
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Handle Incoming Tasks
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-quickstart). [Full Markdown](../../../../../docs/sdks/webex-contact-center-web-sdk-quickstart.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Welcome to the Quick Start Guide for the Webex Contact Center (WxCC) SDK.

---

This guide is designed to help developers quickly set up, authenticate, and interact with the WxCC SDK. By following this guide and integrating the provided code snippets, you'll be able to log in an agent, manage agent states, and handle incoming tasks efficiently. Let's get started!

## Selected section

## Handle Incoming Tasks

To listen for incoming calls or tasks:

```js
webex.cc.on('task:incoming', (task) => {
  console.log('Incoming task:', task);
  // Use the task object received in this event to call the task APIs
});

webex.cc.on('task:hydrate', (task) => {
  console.log('task:hydrate: ', task);
// This is used when a relogin or reload occurs while an active task is present.
});

webex.cc.on('task:assigned', (task) => {
  console.info('Task accepted: ', task.data.interactionId);
});
```
