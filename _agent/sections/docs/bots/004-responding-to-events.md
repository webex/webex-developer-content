---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bots
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Responding to Events
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bots). [Full Markdown](../../../../docs/bots.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Give Webex users access to outside services right from their Webex spaces. Bots help users automate tasks, bring external content into the discussion, and gain efficiencies.

[Create a Bot](<https://developer.webex.com/my-apps/new/bot>)

## Selected section

## Responding to Events

After creating a bot, you can use its access token with the Webex REST APIs to perform actions as the bot, such as [sending a message](https://developer.webex.com/docs/api/v1/messages/create-a-message) with an interactive [card](https://developer.webex.com/docs/buttons-and-cards) to someone. To respond to events within Webex, such as someone sending your bot a message or adding it to a group space, you'll need to configure webhooks. Webhooks will let you know when an activity has occurred so you can take action. Check out the [Webhooks Guide](https://developer.webex.com/docs/webhooks) for more information about configuring webhooks.

With cards, you can give your users even more ways to interact with your bot or service, right in the Webex clients. Use the [Buttons and Cards Designer](https://developer.webex.com/buttons-and-cards-designer) to quickly create and prototype cards for your bot. See the [Buttons and Cards Guide](https://developer.webex.com/docs/buttons-and-cards) for more information about cards.
