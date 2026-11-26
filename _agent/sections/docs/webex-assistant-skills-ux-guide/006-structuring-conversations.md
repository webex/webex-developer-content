---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-assistant-skills-ux-guide
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Structuring Conversations
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

## Structuring Conversations

Conversations with your skill, like any conversation you'd have with a friend or colleague, follow a conversational structure. Let's look at the pieces of a conversation that will allow users to have great conversations with your skill:

- Intro
- Talking with the User
- In-Skill Help
- Hints
- Outro


Usually there will be a start to the conversation, some back and forth, and a goodbye. We'll refer to these as the 'intro,' 'talking with the user'. and the 'outro'. We also recommend including in-skill help, hints, and error handling. In-skill help instructs users about what your skill can do and hints are on-screen help to guide users. These typically won't all appear in one conversation, but each piece is important to create a robust skill.

### Intro

When a user opens your skill, it's helpful to offer a greeting and let the user know what the skill can do. We recommend including the skill name and a high-level example in your intro. To keep things conversational, we also recommend that your skill be in listening mode after speaking the intro, and that the intro ends with a question to let users know you're ready for their input:

<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte37071e600490842/634f6d96bbff0b3fd98e1caa/skill-icon.png" alt="Skill icon" style="vertical-align: middle; padding-right: 10px;">Weather skill: "_Welcome to the &lt;skillname> skill! I can help you &lt;action> and &lt;action>. What can I do for you?_"

Our example skill, the Weather skill, can tell you today's forecast, tomorrow's forecast, and the temperature. Here's what an introduction for that skill might sound like:

<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte0773407457c5067/634f6d961e79f1285f688603/shout.png" alt="User icon" style="vertical-align: middle; padding-right: 10px;">User: "_OK Webex, open Weather_"

<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte37071e600490842/634f6d96bbff0b3fd98e1caa/skill-icon.png" alt="Skill icon" style="vertical-align: middle; padding-right: 10px;">Weather skill: "_Welcome to the Weather skill! I can help you check the forecast and temperature. What can I help you with_"

### Talking with the User

Your skill will interact with your users by replying or having a back-and-forth conversation. In this section, we'll make recommendations for structuring conversations to communicate effectively and get the information you need to be able to help.

Users start having a conversation with your skill after they invoke it with the skill invocation phrase. After your skill is invoked, it's time to start conversing with your user.

When you're thinking about having a conversation with your user, you'll first need to think about what you want to accomplish with your skill. What will it help users do? The tasks that you'll help your users with are your skill's use cases. First, make a list of your use cases. For example, if we're developing a skill that helps users get weather information, you might have the following use cases:

- Check the weather: get the weather for the user's current location
- Check the weather somewhere else: get the weather for another location


Next, list the information you need from the user to fulfill these requests. To check the weather, we need to know where the user is. For now, let's assume that we already know where the user is. When you don't need information from the user, your skill can fulfill the user's request in a single turn:

<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte0773407457c5067/634f6d961e79f1285f688603/shout.png" alt="User icon" style="vertical-align: middle; padding-right: 10px;">User: "_OK Webex, ask Weather to get me today's forecast_"

<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte37071e600490842/634f6d96bbff0b3fd98e1caa/skill-icon.png" alt="Skill icon" style="vertical-align: middle; padding-right: 10px;">Weather skill: "_OK! Today's forecast for San Francisco is a high of 75°and a low of 56°_"

What about when you do need information from the user? In our example, the "check weather somewhere else" feature requires that the skill know where "somewhere else" is. When you need information from the user, we recommend that your skill ask the user for the required information. This is a great way to make your skill feel more conversational, and it helps users learn what your skill needs to be able to complete a request.

<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte0773407457c5067/634f6d961e79f1285f688603/shout.png" alt="User icon" style="vertical-align: middle; padding-right: 10px;">User: "_OK Webex, ask Weather to show the weather for somewhere else_"

<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte37071e600490842/634f6d96bbff0b3fd98e1caa/skill-icon.png" alt="Skill icon" style="vertical-align: middle; padding-right: 10px;">Weather skill: "_Where would you like me to check the weather?_"

<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte0773407457c5067/634f6d961e79f1285f688603/shout.png" alt="User icon" style="vertical-align: middle; padding-right: 10px;">User: "_New York_"

<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte37071e600490842/634f6d96bbff0b3fd98e1caa/skill-icon.png" alt="Skill icon" style="vertical-align: middle; padding-right: 10px;">Weather skill: "_OK! Today's forecast for New York is a high of 52° and a low of 33°_"

Webex recommends using questions and multiple turns between the user and your skill to make the experience engaging. This also helps avoid scenarios where the user doesn't know what to provide, and your skill fails because it doesn't have the necessary information. For example, if checking the weather somewhere else didn't ask a follow-up question, your interaction might look like this:

<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte0773407457c5067/634f6d961e79f1285f688603/shout.png" alt="User icon" style="vertical-align: middle; padding-right: 10px;">User: "_OK Webex, check the weather somewhere else_"

<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte37071e600490842/634f6d96bbff0b3fd98e1caa/skill-icon.png" alt="Skill icon" style="vertical-align: middle; padding-right: 10px;">Weather skill: "_Hmmm, I can't check the weather somewhere else unless I know where to check._"

In this interaction, there's no dialogue between the user and the skill, and it forces the user to re-start the conversation. When you need information from your user to complete their request, we recommend asking a question or a series of questions to get the information.

### In-Skill Help

In-skill help is an important part of the conversation flow&mdash;it's how users will learn what your skill offers. We recommend creating an intent to capture different types of in-skill help queries like "How can you help me?" and "What can you do?".

We recommend that your in-skill help reply be a one-sentence summary that highlights your skill's key functionalities. There's no built-in UI for in-skill help, but if you'd like to show a web view or create something, please do. Even if you choose to show something on-screen, it's helpful if it's accompanied by a help reply that includes the skill name and 1-3 short examples.

The Weather skill can tell you the forecast and current temperature. In-skill help for the Weather skill might sound like:

<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte37071e600490842/634f6d96bbff0b3fd98e1caa/skill-icon.png" alt="Skill icon" style="vertical-align: middle; padding-right: 10px;">Weather skill: "_The Weather skill can help you check today's forecast and give you the current temperature._"

Note that in-skill help is different from the Webex Assistant Skills help page. In-skill help is specific to your skill and is where you showcase your skill's features. The Webex Assistant Skills help page only shows a list of the available skills. In the future, we hope to provide a way for you to add your skill to our help view. For now, use in-skill help to show off what your skill can do.

### Hints

Because users typically don't fully understand an AI's capabilities or the right way to frame a query, they often aren't clear on how they can talk to it. Showing hints while your users are talking to your skill can help solve this problem.

**1. What Is a Hint**

A hint is a short piece of text displayed on the UI that suggests voice commands to the user. Hints can appear when the assistant is listening or not listening. Unlike replies, hints are never spoken by the assistant. They're an on-screen example to help nudge users in the right direction.

Webex Assistant usually shows hints when the assistant is listening. After the user says "OK Webex," the assistant wakes up and, while listening, shows a hint of an action the user might take. In the example below, since we don't have any context, we show a generic hint: "call John Smith."

![Generic hint without context](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltc0d5883a2ec2e440/63507e3eb3f39b38fccfe88c/hints.jpg)

We recommend showing a generic hint when your skill is in listening mode. For example, the Weather skill might show a hint like this:

<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte37071e600490842/634f6d96bbff0b3fd98e1caa/skill-icon.png" alt="Skill icon" style="vertical-align: middle; padding-right: 10px;">Weather skill: "_Try saying 'Show today's forecast'._"

By displaying a hint, we can promote the assistant's capabilities and offer something for users to play with. We've learned that when it comes to voice products, people learn best by playing around with them.

**2. How to Use Hints**

The most helpful hints indicate the main ways your user can interact with your skill and are relevant in the current context. For example, when users use Webex Assistant's 'call by name' feature, the hints displayed change depending on the context.

![Hint example](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt16576ae2206e9f16/635080028e2325105d7cc63e/hints_2.png)

When a user lands on the first page of the option carousel, we show "option 1" and "show more." This helps users understand how they can make a selection or scroll through the carousel to see more options.

![Hint example](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt86d9a1e118e15de1/635080968e2325105d7cc642/hints_3.png)

On the second page of the carousel, we show "option 5" and "go back." It wouldn't make sense to keep "option 1" since that option is no longer visible. Displaying "go back" instead of "show more" helps the user learn how to return to the previous screen.

We recommend that you leverage hints in this same way: update your hints to be relevant to what your skill is displaying or what flow it's currently in. Suggested actions, next steps, and navigation tips are all great ways to use hints.

The hints that you show when the assistant isn't listening are very important. If the skill is going to dismiss itself after giving a response, we suggest adding "_To use this skill again, just say "OK Webex, ask &lt;your skill name>..."_. That way your users understand that they'll have to include the skill's name in their query to interact with your skill again. Educating users about how and when to use the skill invocation phrase is crucial.

While hints are great for educating your users about what your skill can do, you should avoid using too many hints at once. This is visually overwhelming and will likely result in users ignoring the hints. We suggest only showing one or two hints at a time to provide suggestions without overwhelming your users.

**3. How to Phrase a Hint** 

Webex Assistant always start hints with "_try saying_". It feels more like a suggestion than a demand, and by keeping the wording and UI style consistent, we help users spot hints easily.

### Outro message

When the user exits the skill, we recommend showing an outro message. An outro helps to acknowledge what the user has said and reminds them to use the skill invocation phrase to interact with your skill again. There are two scenarios where you should consider adding an outro message:

- **The user explicitly asked to exit the skill** &mdash; Similar to how a user can say "_OK Webex, dismiss_" to make the assistant go away, you should allow your users to dismiss your skill as they wish. When they do, we suggest using an outro message, like, "_**Thanks for using &lt;skill_name>!**_", followed by a hint, like, "**_To use this skill again, just say 'OK Webex, ask &lt;skill_name>...'_**"


    The first half of this outro makes the experience more conversational, while the second half helps make it clear to the user that if they want to ask the skill for something, they'll have to start the interaction again. This helps to train users on the difference between interacting with the regular Webex Assistant and your skill.

- **Your skill is going to stop listening and dismiss itself** &mdash; In some cases, when the conversation ends, your skill might stop listening and go away after giving a response. For example:


    <img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte0773407457c5067/634f6d961e79f1285f688603/shout.png" alt="User icon" style="vertical-align: middle; padding-right: 10px;">User: "_OK Webex, ask Weather, what's the weather in San Francisco?_"<br>
    <img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte37071e600490842/634f6d96bbff0b3fd98e1caa/skill-icon.png" alt="Skill icon" style="vertical-align: middle; padding-right: 10px;">Weather skill: "_Today in San Francisco, it's 73 degrees and sunny! To use this skill again, just say "OK Webex, ask <skill_name>_"
