---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-assistant-skills-ux-guide
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Writing Natural Language Responses
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

## Writing Natural Language Responses

So far, we've explored the high-level structure of conversations. This section will provide some specific tips for the replies that make up those conversations.

When users talk with your skill, they'll ask for something and your skill will reply. The replies that the user hears from your skill are called Natural Language Responses (NLRs). These responses aren't just a receipt of an action that has taken place &mdash; they're a core part of the experience.

Responses should be efficient, natural, and consistent to achieve the best user experience. In this section, we'll make recommendations for the length, flow, tone, and word choice of your skill's replies.

### NLR Length

Responses should be as brief as possible, without sacrificing naturalness or causing the tone to sound clipped or brusque. You should communicate the information that the user needs—no more and no less. Ideally, you should be able to say your response in one breath. Brevity in your responses is important because it makes the information easier for users to understand, and there's a limited amount of space on-screen. To avoid overflow in the UI, responses shouldn't be longer than 130 characters.

### Conversational Flow

In natural conversation, we use words that mark the conversation flow, which makes it easier for the listener to follow along. Your Webex Assistant Skill should do the same. This includes markers to affirm what the user has said, mark the steps the user needs to take, or indicate a difference between your skill and the user's expectations.

**1. Use an affirmation when the NLR confirms a response**

Using an affirmation at the beginning of the reply lets the user know that your skill understood their request and is continuing the conversation based on the information from the user. 

Affirmation markers include phrases such as "**ok**" "**got it**" "**sure**" or "**sure thing**". For example, consider the following query:

<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte0773407457c5067/634f6d961e79f1285f688603/shout.png" alt="User icon" style="vertical-align: middle">User: "_OK Webex, ask Weather to show San Francisco forecast_"

&#10005;&nbsp;<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte37071e600490842/634f6d96bbff0b3fd98e1caa/skill-icon.png" alt="Skill icon" style="vertical-align: middle"> Weather skill: "_Here is the weather_"

&#10003;&nbsp;<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte37071e600490842/634f6d96bbff0b3fd98e1caa/skill-icon.png" alt="Skill icon" style="vertical-align: middle"> Weather skill: "_OK! Here's the weather"_"

**2. Use timeline markers when explaining steps**

When instructing the user, it's helpful to use timeline markers to guide them through steps or actions that they need to take, or to add continuity when giving the user a lot of information. When users know how much information is coming, it helps them to better take in that information.

Timeline markers include "**first**," "**next**," "**then**," and "**finally**".

<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte0773407457c5067/634f6d961e79f1285f688603/shout.png" alt="User icon" style="vertical-align: middle">User: "_OK Webex, ask Weather for next week's forecast_"

&#10005;&nbsp;<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte37071e600490842/634f6d96bbff0b3fd98e1caa/skill-icon.png" alt="Skill icon" style="vertical-align: middle"> Weather skill: "_Here is the forecast: Monday and Tuesday are going to be warm. Wednesday is going to cool down some and there might be rain. Thursday is going to warm back up. On Friday it will rain again._"

&#10003;&nbsp;<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte37071e600490842/634f6d96bbff0b3fd98e1caa/skill-icon.png" alt="Skill icon" style="vertical-align: middle"> Weather skill: "_Here's the forecast: Early in the week, it's going to be warm. Then, it'll cool down and there might be some rain Wednesday. Thursday heats back up and finally, on Friday we'll be back to rain._"

**3. Use "Hmmm" to indicate a mismatch in user expectations**

This marker serves as the opposite of an affirmation marker. It lets users know that there is some misunderstanding between your skill and what the user is asking. This can occur when the system isn't able to do something the user asks, or the users asks for something that doesn't match with the state your skill is in. Adding this marker can also make your skill sound less brusque.

For example, consider the following user request to close a web view when there isn't one open:

<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte0773407457c5067/634f6d961e79f1285f688603/shout.png" alt="User icon" style="vertical-align: middle">User: "_OK Webex, ask Weather to close the web view_"

&#10005;&nbsp;<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte37071e600490842/634f6d96bbff0b3fd98e1caa/skill-icon.png" alt="Skill icon" style="vertical-align: middle"> Weather skill: "_The web view isn't open_"

&#10003;&nbsp;<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte37071e600490842/634f6d96bbff0b3fd98e1caa/skill-icon.png" alt="Skill icon" style="vertical-align: middle"> Weather skill: "_Hmmm, there isn't a web view open right now_"

### Tone

Your skill's tone should be friendly, professional, and polite. Webex Assistant and its skills are part of an enterprise assistant, so be sure to make your tone friendly, but not overly casual. Think of the tone as business casual. For example, when greeting a user the skill should avoid being too casual (e.g. "Hey! What's new in your life today?") or too formal (e.g. "Greetings").

&#10005;&nbsp;<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte37071e600490842/634f6d96bbff0b3fd98e1caa/skill-icon.png" alt="Skill icon" style="vertical-align: middle"> Too casual "_Hey! What’s new in your life today?_"

&#10005;&nbsp;<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte37071e600490842/634f6d96bbff0b3fd98e1caa/skill-icon.png" alt="Skill icon" style="vertical-align: middle"> Too formal "_Greetings_"

&#10003;&nbsp;<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte37071e600490842/634f6d96bbff0b3fd98e1caa/skill-icon.png" alt="Skill icon" style="vertical-align: middle"> Just right "_How are you this afternoon?_"

While the first example is friendly, it might be overly so. The second is a formal greeting and sounds a bit terse. Asking a simple question strikes the correct balance here.

Here’s an example for asking the user to choose an option:

&#10005;&nbsp;<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte37071e600490842/634f6d96bbff0b3fd98e1caa/skill-icon.png" alt="Skill icon" style="vertical-align: middle"> Too casual "_Pick an option._"

&#10005;&nbsp;<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte37071e600490842/634f6d96bbff0b3fd98e1caa/skill-icon.png" alt="Skill icon" style="vertical-align: middle"> Too formal "_You can pick someone from these options._"

&#10003;&nbsp;<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte37071e600490842/634f6d96bbff0b3fd98e1caa/skill-icon.png" alt="Skill icon" style="vertical-align: middle"> Just right "_Which option would you like?_"

Phrasing the reply as a question sounds much more natural than commanding the user to make a selection. Questions can help users feel like they’re having a conversation with your skill, rather than the skill just needing to get information from them.

### Word Choice

When using a Webex Assistant Skill, users should feel like they’re talking with a person, not a robot. Colloquial language helps the responses feel more natural. When writing replies for your skill, think about how you would talk when chatting with a non-technical friend.

Here are some ways you can make your replies feel more natural:

**1. Use contractions** &mdash; Contractions are an easy way to make your replies feel more natural. It’s a small change, but one that makes a difference when hearing the spoken reply.

&#10005;&nbsp;<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte37071e600490842/634f6d96bbff0b3fd98e1caa/skill-icon.png" alt="Skill icon" style="vertical-align: middle"> "_I cannot help you with that right now_"

&#10003;&nbsp;<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte37071e600490842/634f6d96bbff0b3fd98e1caa/skill-icon.png" alt="Skill icon" style="vertical-align: middle">"_I can’t help you with that right now_"

**2. Use pronouns** &mdash; Use pronouns like “this,” “that,” “here’s,” and “it” to refer to nouns you’ve already mentioned. If you repeat the noun over and over, it begins to sound strange. If your skill mentions the same entity multiple times, we recommend making the subsequent mentions pronouns.

<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte0773407457c5067/634f6d961e79f1285f688603/shout.png" alt="User icon" style="vertical-align: middle">User: "I_'d like to book this room_"

&#10005;&nbsp;<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte37071e600490842/634f6d96bbff0b3fd98e1caa/skill-icon.png" alt="Skill icon" style="vertical-align: middle">"_OK! I can book this room for you. Would you like me to book this room for you?_"

&#10003;&nbsp;<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte37071e600490842/634f6d96bbff0b3fd98e1caa/skill-icon.png" alt="Skill icon" style="vertical-align: middle">"_OK! I can book this room for you. Would you like me to book it?_"

**3. Avoid technical language and technical abbreviations** &mdash; We recommend leaving abbreviations and jargon out of your skill’s reply. Users don’t know, and probably don’t want or need to know, specific details. Just share what impacts them, like whether they’re able to use a certain feature.

&#10005;&nbsp;<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte37071e600490842/634f6d96bbff0b3fd98e1caa/skill-icon.png" alt="Skill icon" style="vertical-align: middle"> "_PSTN calling is not supported on this device._"

&#10003;&nbsp;<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte37071e600490842/634f6d96bbff0b3fd98e1caa/skill-icon.png" alt="Skill icon" style="vertical-align: middle">"_Dialling phone numbers isn’t currently supported on this device._"

**4. Use "any" instead of "no" in negated sentences** &mdash; Negated sentences with "no" are correct, but sound more formulaic, like reading logic. We recommend using contracted negation rather than "no."

&#10005;&nbsp;<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte37071e600490842/634f6d96bbff0b3fd98e1caa/skill-icon.png" alt="Skill icon" style="vertical-align: middle"> "_This is no incoming call._"

&#10003;&nbsp;<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte37071e600490842/634f6d96bbff0b3fd98e1caa/skill-icon.png" alt="Skill icon" style="vertical-align: middle">"_There isn't an incoming call to answer._"

**5. Use “I” when your skill completes an action** &mdash; If your skill performed an action, use a response that uses “I” as the subject to show that your skill is the one who has completed the action. This gives the user the feeling that your skill has succeeded, which builds credibility.

&#10005;&nbsp;<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte37071e600490842/634f6d96bbff0b3fd98e1caa/skill-icon.png" alt="Skill icon" style="vertical-align: middle"> "_There are 2 meetings._"

&#10003;&nbsp;<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte37071e600490842/634f6d96bbff0b3fd98e1caa/skill-icon.png" alt="Skill icon" style="vertical-align: middle">"_I found 2 meetings_"
