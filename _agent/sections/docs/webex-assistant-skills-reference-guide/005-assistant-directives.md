---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-assistant-skills-reference-guide
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Assistant Directives
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

## Assistant Directives

A **directive** is single instruction, expressed in JSON, sent from the skill or **Assistant NLP** to a **Webex Client**. Each directive will perform some `action` or display a `view` to the **Actor**. The skill is expected to send a list of directives to the **Webex Client** in response to each query the **Actor** asks. The directives are completed in the order
that they are received.

Each individual directive JSON has at least two fields, `name` and `type` and an optional third, `payload`.
- ``name``: the identifier of the directive. The `name` is used by the **Webex Client** to determine which directive is being invoked.
- ``type``: can be either `view` or `action`. These values are defined in advanced by the directive.
- ``payload``: the specification of what the directive will do. If needed, each directive `payload` has an expected structure of key-value pairs. 

This is an example of a `reply` directive.
```json
{
  "name": "reply",
  "type": "view",
  "payload": {
    "text": "Hello, World!"
  }
}
```



> **Info**
>
> When creating a set of directives from your skill, you **must** end the set with either a `listen`  or `sleep` directive. This is the proper way to allow **Webex Assistant** to handle follow-up queries or end user interactions.



### Assistant Directive Examples

The following are the supported directives that a skill can send to the **Webex Client**:

### reply

Type: `view`

Display a text message. The payload contains a text field.

#### Sample Payload

```json
{
  "text": "Hello, World!"
}
```

### speak

Type: `action`

Read a given text aloud.

#### Sample Payload

```json
{
  "text": "Hello, World!"
}
```

### listen

Type: `action`

Listen for a user's response.

**Note:** `payload` is not required.

### sleep

Type: `action`

Dismiss Webex Assistant and end the interaction with the skill. The payload contains an optional `delay` integer value of time that will be waited before dismissing the Assistant. The `delay` can be used to allow a view to be displayed for a duration before being removed from the screen.

#### Sample Payload

```json
{
  "delay": 0
}
```

### ui-hint

Type: `view`

Display text messages containing a suggested response for the user. This text will be styled slightly differently in
the user interface. The payload contains a `text` field containing an array of hints, and an optional `prompt` field denoting
the prompt to display.

#### Sample Payload

```json
{
  "text": ["Hello", "What can you do?"],
  "prompt": "Try saying"
}
```

### asr-hint

Type: `action`

Send a list of words to the Automatic Speech Recognition (ASR) service to help with speech-to-text recognition.
This is intended to help bootstrap the ASR service if commonly used words for your Skill are consistently being
mistranscribed. The payload contains a `text` field containing an array of strings.

#### Sample Payload

```json
{
  "text": ["Hello", "Echo"]
}
```

### display-web-view

Type: `action`

Displays the specified url in a web view on the **Webex Client**. The payload contains an optional `title` field, which is displayed on the web view and a required `url` field of the web page to be displayed. Displayed web views remain on screen until dismissed with a `clear-web-view` directive from your **skill** or by the user interacting with the **Webex Client**.

**Note:** Webex Device web engine must be enabled on each device in order to display the web view. More information can be found [below](https://developer.webex.com/docs/webex-assistant-skills-reference-guide#assistant-skills-and-web-views).

### Sample Payload

```json
{
  "title": "Google",
  "url": "https://google.com"
}
```

### clear-web-view

Type: `action`

Dismisses any web views displayed on **Webex Client**.

**Note:** `payload` is not required.

### assistant-event

Type: `action`

A generic event sent to **Webex Assistant** and forwarded to the **Webex Client**. This directive can be used in combination with [Webex Device Macros](https://help.webex.com/en-US/article/np8b6m6/Use-of-Macros-with-Room-and-Desk-Devices-and-Webex-Boards). A walk through on using macros can be found below. The payload contains a required `name` field and an optional inner `payload` field must be an object if included.

```json
{
  "name": "test",
  "payload": { "foo": "bar" }
}
```
