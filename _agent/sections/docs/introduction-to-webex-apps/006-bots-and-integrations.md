---
type: Excerpt
canonical_url: https://developer.webex.com/docs/introduction-to-webex-apps
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Bots and Integrations
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/introduction-to-webex-apps). [Full Markdown](../../../../docs/introduction-to-webex-apps.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](001-prerequisites.md)

## Article introduction

This tutorial provides an introduction to Webex's extensibility.

---

In this introduction to the Webex REST API, you will use the interactive documentation to experience Webex programmability. The tutorial will then go through a few use-cases, and drill into the fundamentals of Webex Apps.

## Selected section

## Bots and Integrations

Here, you will see how your application can run on behalf of other Webex Users.

Suppose you’re building an "Out of Office Assistant" application that automatically responds to Webex messages on behalf of pre-registered users while they are away. Webex users will authorize your app to screen their messages and respond on their behalf when they are mentioned.

This type of application is called as **Webex Integration**. The Webex integrations use the OAuth Grant Flow protocol to issue the access tokens that can act under Webex users' identities. These tokens are scoped: Limited to the set of authorizations granted by the Webex users themselves.

![apps](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt3a045a22da62f6c6/61bb5cebe5a70e7d5276b582/step5-access-tokens.png)

Suppose you want your Out Of Office Assistant to behave a little differently: Any user could invite the assistant into a Webex space and interact with it like this:
“@OutOfOffice is Mandy on vacation?” or “@OutOfOffice note that I'll be away for the next 2 weeks”.

In that case, you would want your *Out Of Office* application to receive and respond to questions using its own identity, not using someone else's identity.

This is where *Bot Accounts* come into play.
Bots are dedicated Webex accounts that act under their identity. They can be added to spaces like any other Webex user. Some differences and restrictions apply. For example, bots MUST be 'mentioned' to receive messages in group spaces.
