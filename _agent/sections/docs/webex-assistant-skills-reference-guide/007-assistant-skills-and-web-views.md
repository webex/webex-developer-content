---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-assistant-skills-reference-guide
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Assistant Skills and Web Views
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

## Assistant Skills and Web Views

In this next section, we will provide more information about the `display-web-view` and `clear-web-view` directives, as well  as an example of how to use them. These directives can create a richer experience for your end-users. The directives use the existing web engine implemented by the Webex Devices, which is based on a standard Chromium browser and supports many features. An extensive list of all the supported features and limitations can be found [here](https://help.webex.com/en-us/article/pdybr5/Best-Practices-For-Using-the-Web-Engine). For more information on how to create web pages that work well with the Webex Device web engine, follow the RoomOS WebEngine Developer Guide found [here](https://roomos.cisco.com/docs/WebEngine.md).

In order to use the directive on Webex Devices, the Web Engine must be configured to be allowed by an admin on each device. For more information on this, see this article [here](https://help.webex.com/en-us/article/7ypsyc/Enable-Web-App-Management-on-Webex-Boards-and-Desk-Pros).

### Web Views on Webex Devices

The `display-web-view` directive allows skills developers to open a web view by providing a specific URL to the webpage and the
`clear-web-view` directive dismisses any web view present on the screen. When using the web views in your skill experience, you
should keep in mind that skills can be used on non-touch enabled Webex devices. For these devices, the web view will have to dismissed
by the `clear-web-view` directive otherwise the page will remain displayed on the screen with the user unable to remove it via touch.

Two ways to avoid this issue are to include the `clear-web-view` directive in any subsequent interactions after a `display-web-view`
has been sent or to create a specific query handler that will return a `clear-web-view` whenever a user attempts to dismiss the view.

### Web View Example

In this example, we will follow similar pattern to the Webex Device Macros example above. Again continuing from where you left off with either the [Simple Skill](https://developer.webex.com/docs/webex-assistant-skills-guide#building-a-simple-skill) or the [MindMeld Skill](https://developer.webex.com/docs/webex-assistant-skills-guide#building-a-mindmeld-skill) described in the [Webex Skills SDK Guide](https://developer.webex.com/docs/webex-assistant-skills-guide), we will add the necessary code changes to get your Skill to send an `display-web-view` directive.

### Assistant Skill Code

In the implemented skill code, navigate to the dialogue handlers and update them with the following code. Using the `responses` module from `webex-assistant-sdk`, add `responses.DisplayWebView()` to the directives array along with the two parameters, `url` and `title`. Similarly, add `responses.ClearWebView()` to the other dialogue handler.

In the following code snippet, the **on** and **off** handlers from the Simple Skill, Switch, are updated to use the `display-web-view` and `clear-web-view`, respectively.

```python
@api.handle(pattern=r'.*\son\s?.*')
async def turn_on(current_state: DialogueState) -> DialogueState:
    new_state = current_state.copy()

    text = 'Ok, turning lights on.'

    new_state.directives = [
        responses.Reply(text),
        responses.Speak(text),

        # 1. Create `display-web-view` directive and include payload
        responses.DisplayWebView("https://cisco.com"),

        responses.Sleep(10),
    ]

    return new_state

@api.handle(pattern=r'.*\soff\s?.*')
async def turn_off(current_state: DialogueState) -> DialogueState:
    new_state = current_state.copy()

    text = 'Ok, turning lights off.'

    new_state.directives = [
        responses.Reply(text),
        responses.Speak(text),

        # 2. Create `clear-web-view` directive
        responses.ClearWebView(),

        responses.Sleep(10),
    ]

    return new_state
```

After adding the few lines to your dialogue handlers, the skill can now open a web view to Cisco's main landing page and clear it later.

### Walk through

Once the skill is updated, you can go through and invoke the skill. Continuing with the Switch skill example, since the **on** handler was updated with the `display-web-view` directive, wake Webex Assistant and say an **on** query.

![Switch Webview On Query](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt63efaa60eb296076/6244ae57d0764c0ed2c6cec7/switch_webview_query_on.png)

The skill will then return the expected `reply` and `speak` directives and the Assistant will execute those.

![Switch Webview On Response](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt1d3b7d4efbb12147/6244ae57949b9a0ea5bc29bb/switch_webview_query_on_response.png)

Then, the Assistant will handle the `display-web-view` directive and display a web view with Cisco's homepage.

![Switch Webview Display](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltea3c04d4a156842b/6244ae577855a50ef193cf44/switch_webview_display_web_view.png)

Next, you can now wake Webex Assistant and say an **off** query to dismiss the web view from the Webex Device.

![Switch Webview Off Query](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltb5c0c37bcba238c7/6244ae578850ee0e8ea0b254/switch_webview_query_off.png)

Again, the Assistant will return the expected `reply` and `speak` directives.

![Switch Webview Display](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt19afc8c6978088ad/6244ae573e3e050eb746d636/switch_webview_query_off_response.png)

Finally, the Assistant will handle the `clear-web-view` directive and dismiss the web page.

![Switch Webview Display](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte7df30740dc61634/6244ae57cd71790ea0065718/switch_webview_clear_web_view.png)
