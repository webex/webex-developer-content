---
type: Article
title: Pollbot is Open Source
canonical_url: https://developer.webex.com/blog/pollbot-is-open-source
content_type: blog
date: '2023-03-03'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/pollbot-is-open-source)

We're pleased to announce that Pollbot is now available as an open-source project that developers can modify to fit their own needs.

### How it works

Pollbot is used for creating polls within Webex spaces. In its current design, if the bot is added to a group space, then it will include every member of that space in any polls that are created in there. If the bot is used in a 1:1 space, then you will be given the option to provide emails for any users you want to have included in the poll. Polls are created using [Buttons and Cards](https://developer.webex.com/docs/buttons-and-cards) that allow for easier user interaction than sending text commands, though that is possible as well.

#### Example of creating a poll in a 1:1 space:

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt317a4beb2ef7fdf7/6401162f8d9f9910878e6880/pollbot_open-source-2.png)

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt5ec1803c1ef8dd39/6401162f26b2ac6bf80eb8e8/pollbot_open-source-3.png)

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltec68fdecda35d4c4/6401162fbddfe71066fce050/pollbot_open-source-4.png)



#### Example of creating a poll in a group space:

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt6a66f2def9408923/6401162f9ac9ae108e9468ff/pollbot_open-source-5.png)

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltc16beac156aa8af0/6401162f112aba108a264176/pollbot_open-source-6.png)

### Pollbot Code Examples

To use this code, you will need to create your own [bot](https://developer.webex.com/docs/bots) and configure its access token in the `.env` file. The [example.env](https://github.com/WebexSamples/Pollbot-OpenSource/blob/d8081c08ef22e6d58d4c87547eb026d398d1f601/example.env#L1) file has a list of required environment variables, both ones you will need to define as well as some universal ones. Once you've provided them in the file you can simply rename it to `.env` and the app will be able to read those variables when you start it.

The app requires three [webhooks](https://developer.webex.com/docs/webhooks) as well, be sure to use your bot token to create them.

1. Resource: messages, Event: created - pointed to the root of where you're hosting the app.<br /> This webhook is triggered when someone sends the bot a message. The payload contains the messageId so the bot is able to [retrieve the message content](https://developer.webex.com/docs/api/v1/messages/get-message-details) in order to process the command.<br />  **Example**: `"targetUrl":"https://example.com"`
2. Resource: attachmentActions, Event: created - pointed to `/cards`.<br />This webhook is triggered when someone clicks an action button the cards, such as the “Create Poll” button. The payload contains an `attachmentActionsId` so the data that was enter into the card and options that were select can be [retrieved](https://developer.webex.com/docs/api/v1/attachment-actions/get-attachment-action-details) and processed.<br />**Example**: `"targetUrl":"https://example.com/cards"`
3. Resource: memberships, Event: all - pointed to `/memberships`.<br />This is used to track membership changes in a space, such as the bot being added/removed to/from spaces and if there is a moderation change in a space.<br />**Example**: `"targetUrl":"https://example.com/memberships"`

This is an example of how the bot currently works when a user clicks the **Create Poll** button on the initial card that's sent, which triggers this [code](https://github.com/WebexSamples/Pollbot-OpenSource/blob/d8081c08ef22e6d58d4c87547eb026d398d1f601/pollbot.py#L197):

```python
else:
    room_type = room_details.body.get("type")
    card_json = self.application.settings['card_builder'].build_question_card(room_id, room_type, person_id)
```

This will then call the [build_question_card](https://github.com/WebexSamples/Pollbot-OpenSource/blob/d8081c08ef22e6d58d4c87547eb026d398d1f601/pollbot/src/card_builder.py#L197) function within `/pollbot/src/card_builder.py` to build the actual card that will ask the user for their question and the possible answers they want to accept.

```python
def build_question_card(self, room_id, room_type, person_id):
    card_json = self.load_card(Settings.create_card)
    if room_type != "direct":
        self.add_options_card(card_json, person_id)
        card_json["body"][4]["actions"][0]["data"].update({"person_id":person_id})
    else:
        container = card_json["body"][1]["items"]
        container[0]["text"] = "**Step 1: What do you want to ask?**"
        container[1]["text"] = "Enter your question and answer choices"
        actions = card_json["body"][3]["actions"]
        actions[0]["title"] = "Next: Select Recipients"
        actions[0]["data"] = {"submit":"next", "person_id":person_id}
        actions.pop(1)
    return self.finalize_card_json(room_id, "Adaptive Card - Create Poll", card_json)
```

It pulls in the `create_card.json` file from `/pollbot/src/cards` and then adds additional details to it that are specific to the user so it can be stored in the database and be tracked by the creators `personId`. After this it returns the updated `card_json` variable and then finalizes the JSON based on if the bot is being use in a group or 1:1/direct space.

```python
    def finalize_card_json(self, room_id, markdown, card_json, direct=False):
        card = {
                "markdown": markdown,
                "attachments": [
                    {
                        "contentType": "application/vnd.microsoft.card.adaptive",
                        "content": card_json
                    }
                ]
            }
        if direct:
            card.update({"toPersonId": room_id})
        else:
            card.update({"roomId": room_id})
        return card
```

Then the card is posted to the space [here](https://github.com/WebexSamples/Pollbot-OpenSource/blob/d8081c08ef22e6d58d4c87547eb026d398d1f601/pollbot.py#L296):

```python
elif card_json != {}:
    yield self.application.settings['spark'].post_with_retries('https://webexapis.com/v1/messages', card_json)
```

Which uses the [post_with_retries](https://github.com/WebexSamples/Pollbot-OpenSource/blob/d8081c08ef22e6d58d4c87547eb026d398d1f601/pollbot/src/spark.py#L304) function in `/pollbot/src/spark.py` to handle any errors if they were to occur, such as being rate limited.

In addition to any code changes you'd like to do, there are also card files that you can modify as well. In them there is a place to define a support link, so your users can contact you should they run into any issues. Feel free to change them to fit your needs. To get started, head over to the [Pollbot OpenSource](https://github.com/WebexSamples/Pollbot-OpenSource) repo on Github.
