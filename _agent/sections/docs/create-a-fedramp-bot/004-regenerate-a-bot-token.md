---
type: Excerpt
canonical_url: https://developer.webex.com/docs/create-a-fedramp-bot
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Regenerate a Bot Token
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/create-a-fedramp-bot). [Full Markdown](../../../../docs/create-a-fedramp-bot.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

While app creation in the commercial environment happens with the push of a button in the developer portal, that approach is replaced with an API call in the FedRAMP environment.

---

A REST command is issued to POST `/applications` with the payload for a bot or integration as desired. Every API call must be authenticated and credentialed just like in the commercial environment, which is done by means of a Bearer token, here called an access token.

## Selected section

## Regenerate a Bot Token

To regenerate the bot's token, send a DELETE request to the Applications API token endpoint (see the Applications API Reference later in this document for more details).

The bot's new access token will be included in the response payload in the `botToken` field.

**Note**: You cannot use the bot's access token to make this request. Instead, use the admin token as in the example above.

### Example Request

```bash
DELETE https://api-usgov.webex.com/v1/applications/{botId}/botToken
```

### Example Headers

```json
Authorization:Bearer<yourtoken>
```

### Example Response Body

```json
{
  "isNative":false, "id":"Y2lzY29z",
  "friendlyId":"my-bot-1234",
  "type":"bot",
  "name":"My Bot",
  "logo":" https://avatar.webexcontent.com/avatar5678",
  "description":"A brief description of the bot",
  "orgId":"Y2lzY29zcGFyazowNGVkLTRlZGUtYWI3ZC1iNWRiNDYyYjgzMzM",
  "botEmail":"myBot@webex.bot", "botPersonId":"Y2lzY29zcGFyazovL3VzL1BFT1BMRS8x",
  "botToken":"<WEBEX_BOT_ACCESS_TOKEN>",
  "isFeatured":false,
  "submissionStatus":"none",
  "createdBy":"Y2lzY29zcGFyaEtYjY0MS1lZTdiYTI5MWYyM2Y",
   "created":"2020-02-29T21:40:51.150Z"
}
```
