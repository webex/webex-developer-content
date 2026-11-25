---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bots
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Differences Between Bots and People
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bots). [Full Markdown](../../../../docs/bots.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Give Webex users access to outside services right from their Webex spaces. Bots help users automate tasks, bring external content into the discussion, and gain efficiencies.

[Create a Bot](<https://developer.webex.com/my-apps/new/bot>)

## Selected section

## Differences Between Bots and People

One key difference between Webex Bots and regular users is that, in group spaces, bots **only have access to messages in which they are mentioned**. This means that `messages:created` webhooks only fire when the bot is mentioned in a space. However bots are on the roster of a space and they do have encryption keys for the space so the pattern of using mentions does not protect other messages in the space from being accessed by a bot in all flows.

Also, [listing messages](https://developer.webex.com/docs/api/v1/messages/list-messages) requires that you specify a special `?mentionedPeople=me` query parameter.

In addition people have a `personId` that must be resolved via /people, bots have a Bot Id and a `personId`. The Bot Id is shown in the apps page and is usually only known to the developer. The bot's `personId` can be looked up via the bot's email address in /people. 

```http
GET /messages?mentionedPeople=me&roomId=SOME_INTERESTING_ROOM
Authorization: Bearer THE_BOTS_ACCESS_TOKEN
```
