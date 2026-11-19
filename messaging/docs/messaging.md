---
type: Guide
title: Messaging | Overview
display_title: Overview
canonical_url: https://developer.webex.com/docs/messaging
content_type: documentation
product_group:
- webex-suite
categories:
- messaging
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/messaging)

Use the Webex Messaging API to list, create, update, and delete messages.

---

Webex is known for its video conferencing and screen sharing, but messaging is a core element of the platform due to the relaxed and straightforward nature of the medium.  Messages are conversational, fluid, and natural without requiring the participants of the chat to be engaged at that very moment.  Participants can review and respond to chats when its convenient to their needs and circumstances.

The Messaging API is an easy-to-use Restful platform that allows you to create, update, and delete messages. Every message is tagged with sender information (who wrote the message) and the local timestamp (what time did they sent it relative to you). Alternatively, you can change the format of the messages sent (between plain text or markdown) or send a file attachment along with your message to the chat room.

To use the Webex REST API, you'll need a Webex account. Our interactive API Reference uses your personal access token from this to ensure that the API calls are done only by you. In REST, each command is represented by a base URL like `/messages` and the HTTP methods `GET`, `POST`, `PUT` and `DELETE` are used to perform tasks such as request data or perform actions on those resources such as configure your device, start video calls from code, create custom In-Room Controls, and deploy Macros on your devices.
