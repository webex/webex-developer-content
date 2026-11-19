---
type: Guide
title: Create a FedRAMP Bot | Consolidated Guide
display_title: Create a Bot
canonical_url: https://developer.webex.com/docs/create-a-fedramp-bot
content_type: documentation
product_group:
- webex-suite
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/create-a-fedramp-bot)

While app creation in the commercial environment happens with the push of a button in the developer portal, that approach is replaced with an API call in the FedRAMP environment.

---

A REST command is issued to POST `/applications` with the payload for a bot or integration as desired. Every API call must be authenticated and credentialed just like in the commercial environment, which is done by means of a Bearer token, here called an access token.

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
