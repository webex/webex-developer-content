---
type: Excerpt
canonical_url: https://developer.webex.com/docs/buttons-and-cards
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- About Buttons and Cards
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/buttons-and-cards). [Full Markdown](../../../../docs/buttons-and-cards.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Limitations](006-limitations.md)

## Article introduction

Give new levels of interactivity to Webex users by adding Buttons and Cards to your apps.

## Selected section

## About Buttons and Cards

Cards are created by including an adaptive card attachment when [posting a new message](https://developer.webex.com/docs/api/v1/messages/create-a-message). Cards can be interactive, soliciting an action from the user, such as submitting a response to a poll; or they may be purely informational, such as displaying current weather conditions.

To make cards interactive, include buttons. Buttons are actions that users can use to open a URL, show another card, or submit data from an input form within the card. Cards may include up to five buttons (actions). If you include an input form, data submitted by a user is encrypted and stored within the Webex platform. You can use [webhooks](https://developer.webex.com/docs/webhooks) to receive notifications for new form submissions. Use the [Webhooks API](https://developer.webex.com/docs/api/v1/webhooks) to create a webhook for the `attachmentActions` resource's `created` event to receive notifications about card actions. Just like other API resources that contain encrypted data, the webhook's body will not include the form submission. After you receive the webhook, you will need to retrieve the form data via the [Attachment Actions API](https://developer.webex.com/docs/api/v1/attachment-actions). See [Handling Requests from Webex](https://developer.webex.com/docs/webhooks#handling-requests-from-webex) in the Webhooks Guide for more information about how to use webhooks with encrypted data.

Here's an overview of how an application uses webhooks, messages, and attachment actions to create interactive cards:

![Card Interactions](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltaeabd05b9eb2e6b3/5ce7fca5a853bc241f1b08d1/Card-Interactions@2x.png)

### Card Abilities

Cards can be used in direct 1:1 spaces or group spaces. When they're sent to a group space, every user in the space can see and interact with it.

If you need to provide feedback to a user after an interaction with a card, you have a few options.
* You could edit the content of the card as a result of the action (currently available only for the cards that doesn't include images, either pre or post edit). [Edit message](https://developer.webex.com/docs/api/v1/messages/edit-a-message) is the driving force behind editing a card.
* You could remove the card and post a message with the result of the action. To remove a card, simply [delete the message](https://developer.webex.com/docs/api/v1/messages/delete-a-message) that contains the card attachment. The card will be removed from the space.
* Or perhaps the card is in a group space where you want multiple people to interact with it, you could send them a 1:1 message after they've interacted with it.





> **Info**
>
> The ability to update card content for cards with images will be released in the future. Stay tuned to our [blog](https://developer.webex.com/blog) for updates.
