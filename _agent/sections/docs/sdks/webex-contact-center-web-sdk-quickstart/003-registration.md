---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-quickstart
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Registration
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-quickstart). [Full Markdown](../../../../../docs/sdks/webex-contact-center-web-sdk-quickstart.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Welcome to the Quick Start Guide for the Webex Contact Center (WxCC) SDK.

---

This guide is designed to help developers quickly set up, authenticate, and interact with the WxCC SDK. By following this guide and integrating the provided code snippets, you'll be able to log in an agent, manage agent states, and handle incoming tasks efficiently. Let's get started!

## Selected section

## Registration

You can only register the agent once the `webex` object is ready. You'll want to attach a listener for the `webex` object's `ready` event and proceed only after that event has fired:

```js
const agentProfile = await webex.cc.register();
// agentProfile is now available for use
```
When the subscription is successful, the `register` method returns a `Profile` object. This object contains details about the agent, such as their ID, name, and current state. This action enables the SDK to receive and handle events from the Contact Center backend, such as incoming tasks, state changes, and other agent-related events. The `Profile` is needed to identify and manage the agent within the Contact Center system.
