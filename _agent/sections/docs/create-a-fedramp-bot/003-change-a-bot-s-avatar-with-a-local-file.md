---
type: Excerpt
canonical_url: https://developer.webex.com/docs/create-a-fedramp-bot
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Change a Bot's Avatar with a Local File
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/create-a-fedramp-bot). [Full Markdown](../../../../docs/create-a-fedramp-bot.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

While app creation in the commercial environment happens with the push of a button in the developer portal, that approach is replaced with an API call in the FedRAMP environment.

---

A REST command is issued to POST `/applications` with the payload for a bot or integration as desired. Every API call must be authenticated and credentialed just like in the commercial environment, which is done by means of a Bearer token, here called an access token.

## Selected section

## Change a Bot's Avatar with a Local File

To change a bot's avatar with a new local file, send a POST request to the Applications API (see Applications API Reference later in this document for more details). Include the new avatar as a `multipart/form-datarequest`.

### Example Multipart Request

```bash
POST https://api-usgov.webex.com/v1/applications/{botId}/logo
```

### Example Headers

```json
Authorization:Bearer<yourtoken>
```

### Example Multipart Request

```bash
curl--requestPOST\
  --header "Authorization:BearerACCESS_TOKEN"\
  --form "logo=@/home/desktop/avatar.png;type=image/png"\
  https://api-usgov.webex.com/v1/applications/{botId}/logo

{
  "isNative":false,
  "id":"Y2lzYmNiNTE2YzA1NmZhYmJiOTA5NWM3MWQ2Y2JjZWRjYTYwNmJh",
  "friendlyId":"my-bot-1234",
  "type":"bot",
  "name":"MyBot",
  "logo":"https://avatar.webexcontent.com/avatar5678",
  "description":"A brief description of the bot",
  "orgId":"Y2lzY29zcGFyazowNGVkLTRlZGUtYWI3ZC1iNWRiNDYyYjgzMzM",
  "botEmail":"myBot@webex.bot",
  "botPersonId":"YXNkZmtiNTE2YzA1NmZhYmJiOTA5NWM3MWQ2Y2JjZWRjYTYwNmJh”,
  "isFeatured":false,
  "submissionStatus":"none",
  "createdBy":"Y2lzY29zcGFyaEtYjY0MS1lZTdiYTI5MWYyM2Y",
  "created":"2020-02-29T21:40:51.150Z"
}
```
