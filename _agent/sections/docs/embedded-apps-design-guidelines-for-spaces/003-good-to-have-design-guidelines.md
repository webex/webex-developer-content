---
type: Excerpt
canonical_url: https://developer.webex.com/docs/embedded-apps-design-guidelines-for-spaces
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Good-to-Have Design Guidelines
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/embedded-apps-design-guidelines-for-spaces). [Full Markdown](../../../../docs/embedded-apps-design-guidelines-for-spaces.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Requirements for In-Space Embedded Apps](001-requirements-for-in-space-embedded-apps.md)

## Article introduction

---

This document provides design and experience guidelines for embedded apps running in a Messaging space, specifically:

- ­­­**Requirements** that in-space embedded apps must meet to be approved for inclusion on Webex App Hub.
* **Recommended design guidelines** that when implemented provide a great experience for users of in-space apps. While not explicitly required, apps that do not incorporate the recommended guidelines may not be approved if it is determined they provide a poor user experience.
* **Good-to-have design guidelines** that when incorporated into embedded apps provide an enhanced user experience, both within the app itself and the larger Webex context.



> **Warning**
>
> Webex App Hub is not supported for Webex for Government (FedRAMP).



See [Embedded Apps Design and Experience Guidelines for Meetings](https://developer.webex.com/docs/embedded-apps-design-guidelines-for-meetings) related to meeting-based apps.

## Selected section

## Good-to-Have Design Guidelines

The following suggestions provide an enhanced user experience both within your app and in the larger Webex context. Incorporating these suggestions is optional and will not block app approval if not implemented.

### Provide a "Freemium" Model for First-time Users

Apps that require users to create an account and select a pricing plan should provide a "freemium" model to allow first-time users an easy sign-up experience. Apps can use the participant's [user ID](https://developer.webex.com/docs/embedded-apps-api-reference#type-definitions) to create a placeholder association between the user and the current app session. This ID is guaranteed to be unique regardless of whether the app has access to the user's personally identifiable information (PII).
