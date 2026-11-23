---
type: Excerpt
canonical_url: https://developer.webex.com/docs/create-a-fedramp-bot
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Delete a Bot
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/create-a-fedramp-bot). [Full Markdown](../../../../docs/create-a-fedramp-bot.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

While app creation in the commercial environment happens with the push of a button in the developer portal, that approach is replaced with an API call in the FedRAMP environment.

---

A REST command is issued to POST `/applications` with the payload for a bot or integration as desired. Every API call must be authenticated and credentialed just like in the commercial environment, which is done by means of a Bearer token, here called an access token.

## Selected section

## Delete a Bot

To delete a bot, send A `DELETE` request to the Applications API (see Applications API Reference later in this document for more details).

The API will respond with an `HTTP 200 OK` response if the bot is successfully deleted.

### Example Request

```bash
DELETE https://api-usgov.webex.com/v1/applications/{botId}
```

### Example Headers

```json
Authorization:Bearer<yourtoken>
```
