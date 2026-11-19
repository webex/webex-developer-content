---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-assistant-skills-ux-guide
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Ending a Conversation
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-assistant-skills-ux-guide). [Full Markdown](../../../../docs/webex-assistant-skills-ux-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

As the developer, Webex Assistant Skills empower you to provide your users with even more voice functionality. In this guide you'll learn about the the high-level ways users will interact with your skill: starting a conversation, continuing a conversation, and ending a conversation.

---



> **Warning**
>
> No new features are being added to Webex Assistant Skills and only skills added through May 2025 are directly supported by Cisco.

## Selected section

## Ending a Conversation

A user's conversations with your skill might come to a natural end, the user might want to end the interaction, or the user may no longer need the assistant to be present. For the latter two cases, there are keywords that allow users to end a conversation with the skill: "**exit**" and "**dismiss**".

Both "exit" and "dismiss" keywords end a conversation, but they have slightly different behaviors. As the developer, you must create the "exit" keyword/intent. The "dismiss" keyword is global, and your skill will inherit it from Webex Assistant.

When users use the "exit" and "dismiss" keywords to end interactions, they'll need to make sure the assistant is listening. As with any other type of query, if the assistant isn't already listening, they'll need to use the wake word and skill invocation phrase.

### Exit keyword

Skills are required to create an "exit" intent. The "exit" keyword should end a conversation and display the skill's outro message, if you've configured one. It's also required that the "exit" keyword close anything that you choose to display on-screen. "Exit" is the preferred way for users to end interactions with your skill because it shows your outro message, which is a helpful way to remind users about how they can use your skill again.

Here’s an example **where** the "exit" keyword is used to close the assistant:

<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte0773407457c5067/634f6d961e79f1285f688603/shout.png" alt="User icon" style="vertical-align: middle; padding-right: 10px;">User: "_OK Webex, ask Weather what the forecast is for this week_"

<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte37071e600490842/634f6d96bbff0b3fd98e1caa/skill-icon.png" alt="Skill icon" style="vertical-align: middle; padding-right: 10px;">Weather skill: "OK, here’s this week’s forecast: On Monday, the highs
will be in the 80s and drop to the 50s in the evening. On Tuesday..._"

<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte0773407457c5067/634f6d961e79f1285f688603/shout.png" alt="User icon" style="vertical-align: middle; padding-right: 10px;">User, interrupting the skill: "OK Webex, tell Weather to exit"

![Skill after exit](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt075bcc7e19cf3888/6352cd6beb4a5478dab70d8a/dismiss.png)

### Dismiss keyword

The "dismiss" keyword will immediately end the conversation, without displaying the outro message. You can think of "dismiss" as a stronger version of "exit." A user might use "dismiss" if they need to end an interaction quickly or something is going wrong. This keyword allows the user to end a non-optimal interaction with ease. Example where the "exit" keyword is used to close the assistant:

<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte0773407457c5067/634f6d961e79f1285f688603/shout.png" alt="User icon" style="vertical-align: middle; padding-right: 10px;">User: "_OK Webex, ask Weather for the forecast in Eventide_"

<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte37071e600490842/634f6d96bbff0b3fd98e1caa/skill-icon.png" alt="Skill icon" style="vertical-align: middle; padding-right: 10px;">Weather skill: "_Hmmm, where should I check the forecast?_"

<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte0773407457c5067/634f6d961e79f1285f688603/shout.png" alt="User icon" style="vertical-align: middle; padding-right: 10px;">User: "Actually, dismiss"
