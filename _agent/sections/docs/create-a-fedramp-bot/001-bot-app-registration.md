---
type: Excerpt
canonical_url: https://developer.webex.com/docs/create-a-fedramp-bot
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Bot – App Registration
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/create-a-fedramp-bot). [Full Markdown](../../../../docs/create-a-fedramp-bot.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

While app creation in the commercial environment happens with the push of a button in the developer portal, that approach is replaced with an API call in the FedRAMP environment.

---

A REST command is issued to POST `/applications` with the payload for a bot or integration as desired. Every API call must be authenticated and credentialed just like in the commercial environment, which is done by means of a Bearer token, here called an access token.

## Selected section

## Bot – App Registration

To create a new bot, send a `POST` request to the Applications API (see Applications API Reference later in this document for more details).

The request must include the

- Application type
- The bot's name
- A unique identifier (`botEmail`)
- An avatar logo (picture)
- A brief description.

The bot's name is the display name of the bot in the Webex client application, whereas the `botEmail` is a unique identifier for the bot that users use when adding the bot to spaces or when finding the bot in the clients. The `botEmail` must end with `@webex.bot`.

The bot's avatar must be included in the initial request to create the bot. If the avatar is publicly accessible, a JSON request body with the avatar's URL may be sent to the API. If the avatar is a local file that needs to be uploaded with the request, the request must be a `multipart/form-datarequest` rather than JSON.

**Note**: After creating a bot, the new bot's access token (`botToken`) is included in the response. Copy the token, keep it somewhere safe, and share it with your app developers. You can generate a new token by regenerating the **botToken** (see Regenerate a Bot Token later in this document for more details).

The bot token is all your developers need to develop bot applications for FedRAMP. More specifically, the bot token is used as the Bearer token to call the rest of the Webex APIs

### Example JSON Request

```bash
POST https://api-usgov.webex.com/v1/applications
```

### Example Headers

```json
Authorization: Bearer <your token>
Content-Type:application/json
```

### Example JSON Request Body

```json
{
  "type":"bot",
  "name":"MyBot",
  "botEmail":"myBot@webex.bot",
  "description": "A brief description of the bot",
  "logo": https://example.com/assets/bot-avatar.png
}
```

### Example Multipart Request with cURL

```bash
curl --request POST \
--header "Authorization: Bearer ACCESS_TOKEN" \
--form"type=bot"\
--form"name=MyBot"\
--form "botEmail=myBot@webex.bot"\
--form"description=Abriefdescriptionofthebot"\
--form "logo=@/home/desktop/avatar.png;type=image/png" \https://api-usgov.webex.com/v1/applications

{
  "isNative":false, "id":"Y2lzYmNiNTE2YzA1NmZhYmJiOTA5NWM3MWQ2Y2JjZWRjYTYwNmJh",
  "friendlyId":"my-bot-1234",
  "type":"bot",
  "name":"MyBot","logo":"https://avatar.webexcontent.com/avatar1234",
  "description":"A brief description of the bot",
  "orgId":"Y2lzY29zcGFyazowNGVkLTRlZGUtYWI3ZC1iNWRiNDYyYjgzMzM",
  "botEmail":"myBot@webex.bot",
  "botPersonId":"YXNkZmtiNTE2YzA1NmZhYmJiOTA5NWM3MWQ2Y2JjZWRjYTYwNmJh”,
  "botToken":"<WEBEX_BOT_ACCESS_TOKEN>",
  "isFeatured":false,
  "submissionStatus":"none",
  "createdBy":"Y2lzY29zcGFyaEtYjY0MS1lZTdiYTI5MWYyM2Y",
  "created":"2020-02-29T21:40:51.150Z"
}
```
