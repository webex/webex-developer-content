---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-assistant-skills-reference-guide
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Assistant Skills and Webex Devices Macros
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-assistant-skills-reference-guide). [Full Markdown](../../../../docs/webex-assistant-skills-reference-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

We will go over the structure of the requests sent to your Skill from the **Assistant Skills** service and the
responses expected to be returned from your Skill.

---



> **Warning**
>
> No new features are being added to Webex Assistant Skills and only skills added through May 2025 are directly supported by Cisco.

## Selected section

## Assistant Skills and Webex Devices Macros

Next, we will give an example of using Assistant skills and Webex Device Macros together. Continuing from where you left off with either the [Simple Skill](https://developer.webex.com/docs/webex-assistant-skills-guide#building-a-simple-skill) or the [MindMeld Skill](https://developer.webex.com/docs/webex-assistant-skills-guide#building-a-mindmeld-skill) described in the [Webex Assistant Skills SDK Guide](https://developer.webex.com/docs/webex-assistant-skills-guide), we will add the necessary code changes to get your Skill to send an `assistant-event` directive and the necessary Device Macro file to handle the directive.

This example will emit the directive with a simple JSON payload containing the skill name and a text string. Remember that the directive payload can include whatever data you wish to send and does not need to be structured the same way as the example. The macro will then take the event and use the xAPI to pop an alert on the device using the skill name as the title and the text string as the message. 

### Assistant Skill Code

In the implemented skill code, navigate to the dialogue handlers and update them with the following code. Using the `responses` module from `webex-assistant-sdk`, add `responses.AssistantEvent()` to the directives array.

In the following code snippet, the **on** handler from the Simple Skill is updated to return an `assistant-event` directive.
```python
@api.handle(pattern=r'.*\son\s?.*')
async def turn_on(current_state: DialogueState) -> DialogueState:
    new_state = current_state.copy()

    text = 'Ok, turning lights on.'
    
    # 1. Create the assistant-event payload
    assistant_event_payload = {
        'name': 'Switch',
        'payload': {
            'text': text,
        },
    }
    
    new_state.directives = [
        responses.Reply(text),
        responses.Speak(text),

        # 2. Create `assistant-event` directive and include payload
        responses.AssistantEvent(payload=assistant_event_payload),

        responses.Sleep(10),
    ]

    return new_state
```

After adding the few lines to your dialogue handler, the skill can now send a directive that can be handled by the following macro.

### Webex Device Macro

Using device admin privileges, navigate to the Macros Editor on the desired endpoint. You can then add the following Javascript code to handle events in a new macro file. The macro listens for Assistant notification events and on those events, the macro will display an alert with the `text` property of the directive payload. You can find additional information on using your Webex Device [here](https://roomos.cisco.com/docs/Introduction.md).

```js
import xapi from 'xapi';

function alert(title, text = '', duration = 5) {
  xapi.Command.UserInterface.Message.Alert.Display({
    Title: title,
    Text: text,
    Duration: duration,
  });
}

xapi.Event.UserInterface.Assistant.Notification.on((event) => {
  const { Name, Payload } =  event;
  const jsonPayload = JSON.parse(Payload);
  alert(Name, jsonPayload.text);
});
```

### Walk through

Once the skill is updated and the macro is uploaded, you can invoke the skill. Continuing with the Switch skill example, since the **on** handler was updated with the new directive, wake Webex Assistant and say an **on** query.

![Switch Query](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt1cff7ef3c0d1f192/6201787d9d6c325fc227ef14/switch_query.png)

The skill will then return the expected `reply` and `speak` directives and the Assistant will execute those.

![Switch Response](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blta88b074a38650807/6201787dd6534f0c057180ec/switch_response.png)

Finally, the Assistant will pass on the `assistant-event` directive to the device, which will use the macro
to handle the event. You will then see the alert displayed on your device. 

![Switch Alert](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt0a81470eda456456/6201787d8b1f312528797b70/switch_alert.png)

Macros are a very powerful tool that will allow developers to extend the functionality of the Webex Assistant
even more than before.
