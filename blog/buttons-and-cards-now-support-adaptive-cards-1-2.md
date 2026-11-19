---
type: Article
title: Buttons and Cards now support Adaptive Cards 1.2
canonical_url: https://developer.webex.com/blog/buttons-and-cards-now-support-adaptive-cards-1-2
content_type: blog
date: '2020-05-20'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/buttons-and-cards-now-support-adaptive-cards-1-2)

We've made several improvements to [Buttons and Cards](https://developer.webex.com/docs/buttons-and-cards) that we're pleased to share with you. Buttons and Cards, which use Microsoft's Adaptive Cards framework, add interactivity to messages in Webex. Starting today, you can now:

1. Design and build cards right here on Webex for Developers with an interactive [Buttons & Cards Designer](https://developer.webex.com/buttons-and-cards-designer)
2. Use new elements and properties from Adaptive Cards 1.2
3. Ensure that cards you've created are well-formed and will be sent without error with instant validation from the Messages API

Let's dig into each of these features.

#### Buttons and Cards Designer

The new [Buttons and Cards Designer](https://developer.webex.com/buttons-and-cards-designer) is now available here on Webex for Developers: <https://developer.webex.com/buttons-and-cards-designer>

The designer lets you design cards with an interactive GUI. Once your card is ready, use the linked JSON to send your card. Spend less time worrying about the card's JSON syntax and spend your energy on more important tasks.

<p>
<img alt="screenshot of interactive Webex Buttons and Cards Designer" style="float:none" src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltc19d4f9402cfff34/5ebeff9b957e405e0990407e/cards-1.2-release_designer-screenshot.png"/>
</p>

#### Support for Adaptive Cards 1.2

Elements and Properties added to your arsenal from the Adaptive Card 1.2 release include:

* `RichTextBlock`
* `TextRun`
* `ActionSet`
* `fontType` for `TextBlock`
* `bleed`, `minHeight` properties for `Container`
* `style`, `bleed`, `minHeight` properties for `ColumnSet`
* `bleed`, `minHeight`, properties for `Column`
* `inlineAction` property for `Input.Text`
* `wrap` property for `Input.Toggle`
* `wrap` property for `Input.ChoiceSet`
* `backgroundImage` property of `adaptiveCard` and container

Here are a few examples of how you might leverage the new 1.2 schema elements.

The `RichTextBlock` and `TextRun` elements provide a set of attributes that give you fine grained control over the formatting of text in a card, enabling cards with text that looks like this:

<p>
<img alt="screenshot of Webex Card with rich text styling and background image" style="float:none" src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt84737fd2570448c6/5ebeff9cb42d3333c95dbb4e/cards-1.2-release_RichTextBlock-screenshot.png" width="412" height="412"/>
</p>

The new `ActionSet` element provides you with freedom to include action buttons anywhere in the card and not just at the end of a card:

<p>
<img alt="screenshot of Webex Card multiple sets of actions" style="float:none" src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt1422f9acadec3794/5ebeff974a28e119db560b1d/cards-1.2-release_ActionSet-screenshot.png" width="412" height="173"/>
</p>

We encourage you to play around with all of the elements that are now available in the new [Buttons and Cards Designer](https://developer.webex.com/buttons-and-cards-designer).

There are still a few Adaptive Card schema elements and attributes which are not supported by Webex:

* `Media`
* `speak` and `verticalContentAlignment` property for Adaptive Cards
* `fallback` and `requires` property on the  Element level
* `height` property for the `ColumnSet`
* `Action.ToggleVisibility` for `ActionSet` or `Actions`

#### Enhanced Validation Support

To help make it more obvious which aspects of the Adaptive Card schema we do and don’t support, we have enhanced the [Messages API](https://developer.webex.com/docs/api/v1/messages) validation for messages with card attachments. Requests that receive an HTTP 200 response will always result in an attempt to render the card, while responses with a non-200 response will not. The endpoint will return 400 responses with clear error messages in cases where your card uses an unsupported “version” field or includes any of the unsupported elements or attributes. If the card's JSON is malformed, you will receive an HTTP 400 response right away.

A few examples can be seen here:

<p>
<img alt="screenshot of Postman encountering an error when attempting to send a card with an unsupported property" style="float:none" src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltc90e59cc8a10d85e/5ec52f2e5e73766852c8e173/cards-1.2-release_property-validation-error.png"/>
</p>

<p>
<img alt="screenshot of Postman encountering an error when attempting to send a card with an unsupported version" style="float:none" src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt71348a3eae4f7cb9/5ec52f3a957e405e09904b97/cards-1.2-release_version-validation-error.png"/>
</p>

We're excited to bring you these new time-saving features for Buttons and Cards. If you have product feedback or if you have any questions, please reach out to [Webex Developer Support](https://developer.webex.com/support).
