---
type: Excerpt
canonical_url: https://developer.webex.com/docs/embedded-apps-for-webex-devices
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Good-to-Have Design Guidelines
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/embedded-apps-for-webex-devices). [Full Markdown](../../../../docs/embedded-apps-for-webex-devices.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Technical Requirements and Limitations](007-technical-requirements-and-limitations.md) [Requirements for Embedded Apps on Devices](008-requirements-for-embedded-apps-on-devices.md)

## Selected section

## Good-to-Have Design Guidelines

The following suggestions provide an enhanced user experience both within your app and in the larger Webex context. Incorporating these suggestions is optional and will not block app approval if not implemented.

### Provide a "Freemium" Model for First-time Users

Apps that require users to create an account and select a pricing plan should provide a "freemium" model to allow first-time users an easy sign-up experience. Apps can use the participant's [user ID](https://developer.webex.com/docs/embedded-apps-api-reference#type-definitions) to create a placeholder association between the user and the current app session. This ID is guaranteed to be unique regardless of whether the app has access to the user's personally identifiable information (PII).
