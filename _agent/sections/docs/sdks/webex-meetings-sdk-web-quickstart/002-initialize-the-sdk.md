---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-quickstart
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Initialize the SDK
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-quickstart). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-web-quickstart.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Welcome to the Quick Start Guide for the Webex Meetings SDK. This guide is designed to provide developers with a concise walkthrough to swiftly set up, authorize, and test the core meeting functionalities within the Meeting SDK. 

---

By following the sequential flow of this document and integrating the provided code snippets, you'll be able to authenticate your application and create and manage your first meetings. Whether you're new to Webex's Meeting SDK or looking to brush up on the basics, this guide ensures a streamlined experience to get you up and running in no time. Let's dive in!

## Selected section

## Initialize the SDK

If you don't already have a Cisco Webex account, visit the [Webex Developer Portal](https://developer.webex.com/) to create your account and retrieve your **access token** from the following page: [Getting and Using your Personal Access Token](https://developer.webex.com/docs/getting-your-personal-access-token).

To create a new `Webex` object, replace `<AUTHORIZATION/BOT TOKEN>` below with your Personal Access Token from the Developer Portal:

```js
const Webex = import(`webex`);
const webex = Webex.init({
  credentials: {
    access_token: `<AUTHORIZATION/BOT TOKEN>`
  }
});
```

You can only create rooms or meetings once the `Webex` object is ready. You'll want to attach a listener for the `Webex` object's `ready` event and proceed only after that event has fired. Here's a complete workflow:

1. Listen for the ready event and log a message.
1. Create a room titled "My First Room".
1. Add Alice and then Bob to the new room.
1. Send a "Hi Everyone" message to all the participants in the room.

```js
// Listen for the ready event
webex.once('ready', () => {
    console.log('Authentication#initWebex() :: Webex Ready');
  });

webex.rooms.create({ title: `My First Room` }).then(room => {
  return Promise.all([
    webex.memberships.create({
      roomId: room.id,
      personEmail: `alice@example.com`
    }),
    webex.memberships.create({
      roomId: room.id,
      personEmail: `bob@example.com`
    })
  ]).then(() =>
    webex.messages.create({
      markdown: `**Hi Everyone**`,
      roomId: room.id
    })
  );
});
```
