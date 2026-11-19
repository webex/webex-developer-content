---
type: Article
title: New Adaptive Card Features for your Webex Bots!
canonical_url: https://developer.webex.com/blog/new-adaptive-card-features-for-your-webex-bots
content_type: blog
date: '2023-09-13'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/new-adaptive-card-features-for-your-webex-bots)

We're excited to announce a groundbreaking update to [Webex Bots](https://developer.webex.com/docs/bots) that enhances their capabilities and provides developers with more creative freedom when designing user interactions. With this latest feature release, [Webex Bots](https://developer.webex.com/docs/bots) now support the inclusion of new properties in the [Adaptive Card](https://developer.webex.com/docs/buttons-and-cards) specification that were previously unsupported. These properties, namely `verticalContentAlignment` and `action.togglevisibility`, open up a world of possibilities for creating richer and more dynamic conversational experiences within the Webex platform.

### Vertical Content Alignment for Improved Layout Control

In the realm of bot-driven conversations, aesthetics and layout play a crucial role in delivering a seamless and engaging experience to users. With the introduction of the `verticalContentAlignment` property in Adaptive Cards, developers can now fine-tune the vertical alignment of content within card elements. When a value is not specified, the `verticalContentAlignment` is inherited from the parent container. If no parent container has `verticalContentAlignment` set, it defaults to “top”. Read more about this property at the [official Adaptive Cards documentation page](https://vnext.adaptivecards.io/explorer/Container.html).

An example you can try with the [Messages API](https://developer.webex.com/docs/api/v1/messages/create-a-message) follows:

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt777ecfff0cd292a3/650095240433c0eaad253b1a/buttons-and-cards-new-properties-2.png)

```json
POST https://webexapis.com/v1/messages
{
  "roomId": "YOUR_ROOM_ID",
  "text": "Card Included",
  "attachments": [
    {
      "contentType": "application/vnd.microsoft.card.adaptive",
      "content": {
        "type": "AdaptiveCard",
        "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
        "version": "1.3",
        "body": [
          {
            "type": "Container",
            "height": "stretch",
            "style": "accent",
            "items": [
              {
                "type": "TextBlock",
                "text": "I'm a regular TextBlock...",
                "wrap": true
              }
            ]
          },
          {
            "type": "Container",
            "style": "good",
            "height": "stretch",
            "items": [
              {
                "type": "TextBlock",
                "text": "But I'm centered...",
                "wrap": true
              }
            ],
            "verticalContentAlignment": "Center"
          },
          {
            "type": "Container",
            "height": "stretch",
            "style": "attention",
            "items": [
              {
                "type": "TextBlock",
                "text": "And l'm like a footer!",
                "wrap": true
              }
            ],
            "verticalContentAlignment": "Bottom"
          }
        ],
        "minHeight": "300px"
      }
    }
  ]
}
```

In the above example, the `verticalContentAlignment` property is set to "Center," ensuring that the text content is vertically centered within the TextBlock element. This level of control allows for better design consistency and ensures that critical information is presented effectively to users.

### Enhanced Interactivity with togglevisibility Action

Interaction is a fundamental aspect of bot conversations, and the `action.togglevisibility` property opens up exciting new possibilities for creating dynamic and user-responsive experiences. This property enables developers to define actions that toggle the visibility of specific card elements, allowing for the presentation of information in a more organized and user-friendly manner. You can also make specific actions for “show” and “hide” elements instead of just toggling. Read more about this property at the [official Adaptive Cards documentation page](https://adaptivecards.io/explorer/Action.ToggleVisibility.html).

An example you can try with the [Messages API](https://developer.webex.com/docs/api/v1/messages/create-a-message) follows:

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt3971f1f1c97b8098/650095249da015085e1ec716/buttons-and-cards-new-properties-3.gif)

```json
POST https://webexapis.com/v1/messages
{
  "roomId": "YOUR_ROOM_ID",
  "text": "Card Included",
  "attachments": [
    {
      "contentType": "application/vnd.microsoft.card.adaptive",
      "content": {
        "type": "AdaptiveCard",
        "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
        "version": "1.3",
        "body": [
          {
            "type": "TextBlock",
            "text": "Click below to toggle details:",
            "wrap": true
          },
          {
            "type": "TextBlock",
            "text": "These details are important!",
            "isVisible": false,
            "id": "detailsText"
          }
        ],
        "actions": [
          {
            "type": "Action.ToggleVisibility",
            "title": "Toggle Details",
            "targetElements": ["detailsText"]
          }
        ]
      }
    }
  ]
}
```

In this example, a "Toggle Details" button is presented to users. When the button is clicked, the `detailsText` TextBlock element toggles its visibility, revealing additional information. This allows for a more streamlined user experience, presenting information only when necessary and reducing clutter.

### Getting Started

To take advantage of these exciting new features, simply update your existing Adaptive Card designs to include the `verticalContentAlignment` property and utilize the `action.togglevisibility` property for interactive toggling. The possibilities are endless, from designing captivating onboarding experiences to creating intuitive menu systems.

We can't wait to see the innovative ways you incorporate these enhancements into your Webex Bots! As always, our developer documentation and community forums are available to assist you in making the most of these new features.

Remember, the future of bot-driven interactions is now, and with these new Adaptive Card properties, the sky's the limit. Upgrade your Webex Bots today and embark on a journey of enhanced creativity and interactivity!

### Need Some Help? We Got You Covered!

We are excited to provide you with support for these features. If you need help, the [Webex Developer Support Team](https://developer.webex.com/support) is standing by and happy to assist. You can also start or join a conversation on the [Webex for Developers Community Forum](https://cs.co/WebexDeveloperCommunity).
