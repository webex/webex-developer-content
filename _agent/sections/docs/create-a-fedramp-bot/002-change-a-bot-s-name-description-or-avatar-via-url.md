---
type: Excerpt
canonical_url: https://developer.webex.com/docs/create-a-fedramp-bot
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Change a Bot's Name, Description, or Avatar (via URL)
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/create-a-fedramp-bot). [Full Markdown](../../../../docs/create-a-fedramp-bot.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

While app creation in the commercial environment happens with the push of a button in the developer portal, that approach is replaced with an API call in the FedRAMP environment.

---

A REST command is issued to POST `/applications` with the payload for a bot or integration as desired. Every API call must be authenticated and credentialed just like in the commercial environment, which is done by means of a Bearer token, here called an access token.

## Selected section

## Change a Bot's Name, Description, or Avatar (via URL)

To change a bot's name, description, or avatar, send a PATCH request to the Applications API (see Applications API Reference later in this document for more details). Include the fields to change and their new values. Only the name, description, and avatar (if publicly accessible via a URL) may be changed with a PATCH request.

### Example JSON Request

```bash
PATCH https://api-usgov.webex.com/v1/applications/{botId}
```

### Example Headers

```json
Authorization: Bearer <your token>
Content-Type:application/json
```

### Example JSON Request Body

```json
{
  "name": "My Awesome Bot",
  "description": "A brief description of the bot.",
  "logo": https://example.com/assets/new-avatar.png
}

{
  "isNative":false,
  "id":"Y2lzYmNiNTE2YzA1NmZhYmJiOTA5NWM3MWQ2Y2JjZWRjYTYwNmJh",
  "friendlyId":"my-awesome-bot-1234","type":"bot",
  "name":"MyAwesomeBot",
  "logo":"https://avatar.webexcontent.com/avatar1234",
  "description":"A brief description of the bot.",
  "orgId":"Y2lzY29zcGFyazowNGVkLTRlZGUtYWI3ZC1iNWRiNDYyYjgzMzM",
  "botEmail":"myBot@webex.bot",
  "botPersonId":"YXNkZmtiNTE2YzA1NmZhYmJiOTA5NWM3MWQ2Y2JjZWRjYTYwNmJh”,
  "isFeatured":false,
  "submissionStatus":"none",
  "createdBy":"Y2lzY29zcGFyaEtYjY0MS1lZTdiYTI5MWYyM2Y",
  "created":"2020-02-29T21:40:51.150Z"
}
```
