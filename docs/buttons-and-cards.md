---
type: Guide
title: Buttons and Cards
display_title: Buttons and Cards
canonical_url: https://developer.webex.com/docs/buttons-and-cards
content_type: documentation
product_group:
- webex-suite
categories:
- messaging
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/buttons-and-cards)

Give new levels of interactivity to Webex users by adding Buttons and Cards to your apps.

## Overview

Buttons and Cards let you add interactivity to Webex messages. Users can interact with your app in rich new ways without ever leaving the Webex client.

![Sample Card](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltad04e62c8a7f9bc5/5d431c4148143c39c4b3e876/Adaptive-Cards-Example@2x.png)

[Bots](https://developer.webex.com/docs/bots) and [Integrations](https://developer.webex.com/docs/integrations) can add cards to Webex spaces by including a card attachment when posting a message. Card attachments use Microsoft's [Adaptive Cards](https://adaptivecards.io) specification to define the content of the card. The Webex clients render cards with the same look and feel across every platform, letting you focus on the content and the interaction without worrying about the presentation.




Design your own card
Experiment with the Button and Cards framework and export a JSON file.
[Try it](<https://developer.webex.com/buttons-and-cards-designer>)

![Buttons and Cards Designer](<https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt886d02019b5774d2/5e3b3a8dc77dbe6512a24f61/buttonsAndCardsDemo.gif>)




## What's New

Support for Version 1.3 properties:
* `isRequired`
* `label`
* `errorMessage`
* `regex` 

Sample JSON for card exhibiting input validation using Version 1.3 properties is as follows:
```json
{
    "type": "AdaptiveCard",
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.3",
    "body": [
        {
            "type": "Input.Text",
            "label": "Name",
            "isRequired": true,
            "placeholder": "First Name + Last Name",
            "errorMessage": "Please provide a valid input",
            "regex": "^[\\p{L} .'-]+$",
            "id": "sample text"
        },
        {
            "type": "Input.Date",
            "id": "sample date",
            "label": "Date of Birth",
            "errorMessage": "Please enter a valid date",
            "isRequired": true,
            "min": "1960-01-01",
            "max": "1999-12-31"
        }
    ],
    "actions": [
        {
            "type": "Action.Submit",
            "title": "Action.Submit"
        }
    ]
}

```

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



## Working with Cards

Buttons and Cards use Microsoft's [Adaptive Cards](https://adaptivecards.io) specification to define the content of the card. To learn more about the specification, see the [documentation](https://docs.microsoft.com/en-us/adaptive-cards/). They also provide a [schema explorer](https://adaptivecards.io/explorer/) to help you create cards. Keep in mind that there are [some elements and attributes that are not supported with Webex](#limitations).

You can design and experiment with Buttons and Cards in our interactive [Buttons and Cards Designer](https://developer.webex.com/buttons-and-cards-designer).



> **Info**
>
> For an introduction to Webex Cards, see the following lab on Cisco DevNet, [Webex Adaptive Cards](https://developer.cisco.com/learning/modules/creating-webex-bots/webex-adaptive-cards/about-adaptive-cards/).



### Action Webhooks

When using the `Action.Submit` action or the `selectAction` attribute of other elements in cards, data that is generated by users is encrypted and stored within the Webex Platform. If you want to receive a notification when users submit data, you'll need to use webhooks. For more information about webhooks in general, see the [Webhooks](https://developer.webex.com/docs/webhooks) guide.

To watch for form submissions use the `attachmentActions` webhooks resource. Only one webhook is needed to receive submission notifications for every card created by your app–this resource does not support any filters.

`POST https://webexapis.com/v1/webhooks`

```json
{
  "name": "My Attachment Action Webhook",
  "targetUrl": "https://example.com/mywebhook",
  "resource": "attachmentActions",
  "event": "created"
}
```

### Creating a Card

To create a card in Webex, include the adaptive card object in the `attachments` parameter of a new message. For help with defining the card's content, see the [Adaptive Cards documentation](https://docs.microsoft.com/en-us/adaptive-cards/).

Here's an example of how to [create a message](https://developer.webex.com/docs/api/v1/messages/create-a-message) that will include a card with a few text blocks, an input form, and an action which will submit the form:

`POST https://webexapis.com/v1/messages`

```json
{
  "roomId": "Y2lzY29zcGFyazovL3VzL1JPT00vYmJjZWIxYWQtNDNmMS0zYjU4LTkxNDctZjE0YmIwYzRkMTU0",
  "markdown": "[Tell us about yourself](https://www.example.com/form/book-vacation). We just need a few more details to get you booked for the trip of a lifetime!",
  "attachments": [
    {
      "contentType": "application/vnd.microsoft.card.adaptive",
      "content": {
        "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
        "type": "AdaptiveCard",
        "version": "1.0",
        "body": [
          {
            "type": "ColumnSet",
            "columns": [
              {
                "type": "Column",
                "width": 2,
                "items": [
                  {
                    "type": "TextBlock",
                    "text": "Tell us about yourself",
                    "weight": "bolder",
                    "size": "medium"
                  },
                  {
                    "type": "TextBlock",
                    "text": "We just need a few more details to get you booked for the trip of a lifetime!",
                    "isSubtle": true,
                    "wrap": true
                  },
                  {
                    "type": "TextBlock",
                    "text": "Don't worry, we'll never share or sell your information.",
                    "isSubtle": true,
                    "wrap": true,
                    "size": "small"
                  },
                  {
                    "type": "TextBlock",
                    "text": "Your name",
                    "wrap": true
                  },
                  {
                    "type": "Input.Text",
                    "id": "Name",
                    "placeholder": "John Andersen"
                  },
                  {
                    "type": "TextBlock",
                    "text": "Your website",
                    "wrap": true
                  },
                  {
                    "type": "Input.Text",
                    "id" : "Url",
                    "placeholder": "https://example.com"
                  },
                  {
                    "type": "TextBlock",
                    "text": "Your email",
                    "wrap": true
                  },
                  {
                    "type": "Input.Text",
                    "id": "Email",
                    "placeholder": "john.andersen@example.com",
                    "style": "email"
                  },
                  {
                    "type": "TextBlock",
                    "text": "Phone Number"
                  },
                  {
                    "type": "Input.Text",
                    "id": "Tel",
                    "placeholder": "+1 408 526 7209",
                    "style": "tel"
                  }
                ]
              },
              {
                "type": "Column",
                "width": 1,
                "items": [
                  {
                    "type": "Image",
                    "url": "https://upload.wikimedia.org/wikipedia/commons/b/b2/Diver_Silhouette%2C_Great_Barrier_Reef.jpg",
                    "size": "auto"
                  }
                ]
              }
            ]
          }
        ],
        "actions": [
          {
            "type": "Action.Submit",
            "title": "Submit"
          }
        ]
      }
    }
  ]
}
```

The content length of the entire message (`text`, `markdown`, and `attachments`) cannot exceed 22740 bytes. You can reduce the size of card attachments by not including whitespace in the card's JSON markup.

Images linked in a card will be downloaded and stored with the message. As a rule of thumb, the overall size of the card's JSON and downloaded images should not exceed 80 kilobytes, but this limit can be lower for cards with several images. Don't send cards with links to more than 10 images.

#### Fallback Text

When sending a card, the Webex message object must include either `text` or `markdown` properties for clients that cannot render cards. This text should give the user context about the card's content and provide an alternative method to interact with the card's actions. It cannot include [@mentions](https://developer.webex.com/docs/api/basics#formatting-messages).

#### Card notificaiton

When a message with a card is sent, a notification is received in the Webex app. The format of the notification is generic `<Person/bot> shared a card` and does not include the `Fallback Text`. Below are examples of card notifications received in the desktop and mobile app respectively.

![Card notifications](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt9e9cb76a4c064baa/cards_notification.png)

### Handling Submissions

If you registered a webhook for the `attachmentActions` webhook resource, your app will receive a webhook with the following envelope and data if a user submits data:

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1dFQkhPT0svOTZhYmMyYWEtM2RjYy0xMWU1LWExNTItZmUzNDgxOWNkYzlh",
  "name": "My Attachment Action Webhook",
  "resource": "attachmentActions",
  "event": "created",
  "orgId": "OTZhYmMyYWEtM2RjYy0xMWU1LWExNTItZmUzNDgxOWNkYzlh",
  "appId": "Y2lzY29zcGFyazovL3VzL0FQUExJQ0FUSU9OL0MyNzljYjMwYzAyOTE4MGJiNGJkYWViYjA2MWI3OTY1Y2RhMzliNjAyOTdjODUwM2YyNjZhYmY2NmM5OTllYzFm",
  "ownedBy": "creator",
  "status": "active",
  "actorId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS83MTZlOWQxYy1jYTQ0LTRmZ",
  "data": {
    "id": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi85NmFiYzJhYS0zZGNjLTE",
    "type": "submit",
    "messageId": "GFyazovL3VzL1BFT1BMRS80MDNlZmUwNy02Yzc3LTQyY2UtOWI4NC",
    "personId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS83MTZlOWQxYy1jYTQ0LTRmZ",
    "roomId": "L3VzL1BFT1BMRS80MDNlZmUwNy02Yzc3LTQyY2UtOWI",
    "created": "2016-05-10T19:41:00.100Z"
  }
}
```

Similar to other webhook resources, the data property of `attachmentActions` webhooks will not contain any sensitive data. You will need to use the `data.id` property to retrieve the attachment action:

`GET https://webexapis.com/v1/attachment/actions/Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi85NmFiYzJhYS0zZGNjLTE`

```json
{
  "type": "submit",
  "messageId": "GFyazovL3VzL1BFT1BMRS80MDNlZmUwNy02Yzc3LTQyY2UtOWI4NC",
  "inputs": {
    "Name": "John Andersen",
    "Url": "https://example.com",
    "Email": "john.andersen@example.com",
    "Tel": "+1 408 526 7209"
  },
  "id": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi85NmFiYzJhYS0zZGNjLTE",
  "personId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS83MTZlOWQxYy1jYTQ0LTRmZ",
  "roomId": "L3VzL1BFT1BMRS80MDNlZmUwNy02Yzc3LTQyY2UtOWI",
  "created": "2016-05-10T19:41:00.100Z"
}
```

## Supported Clients

The following Webex clients and SDKs support Buttons and Cards:

* Desktop Clients: Windows and Mac
* Mobile Clients: Android and iOS
* [Web Client](https://web.webex.com/)
* [Browser SDK](https://developer.webex.com/docs/sdks/browser)
* [Widgets](https://developer.webex.com/docs/widgets#space-widget)



> **Info**
>
> Watch our [blog](https://developer.webex.com/blog) for news about Buttons and Cards support in our other clients and SDKs.



## Limitations

* Webex supports Adaptive Cards Version 1.3.
* The following card elements are not supported: `Media`.
* The following card properties are not supported: `fallback` for card elements, `fallbackText`, `requires`, and `speak`.
* The `height` property of the `ColumnSet` element is not supported.
* Cards may include up to twenty actions (using `ActionSet` gives you more freedom).
* Only one card can be sent per request.
* Editing of Cards on User interaction is possible only for cards with no images, pre or post Edit.
* Images in the SVG are not supported.
