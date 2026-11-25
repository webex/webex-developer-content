---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-assistant-skills-ux-guide
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Error Handling
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

## Error Handling

There will be times when your skill won’t be able to handle everything, and that’s okay. To give your users the best experience, we recommend having various error messages and opportunities for the user to try again. This helps users understand what’s happening and, ideally, allows them to recover from the error.

**1. Skill Error**

_Issue_: The user asks for something that your skill can do, but the skill can't complete the request.

Sometimes your skill might encounter an issue. Let your user know that your skill is experiencing an issue processing requests and that they should try again later.

<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte0773407457c5067/634f6d961e79f1285f688603/shout.png" alt="User icon" style="vertical-align: middle; padding-right: 10px;">User: "_OK Webex, ask Weather to check the temperature_"<br>
<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte37071e600490842/634f6d96bbff0b3fd98e1caa/skill-icon.png" alt="Skill icon" style="vertical-align: middle; padding-right: 10px;">Weather skill: "_Hmmm. Something went wrong. Try again later._"

**2. Unknown Request**

_Issue_: The user asks for something your skill doesn’t support.

When a user asks for something that your skill can't do, you can use a generic error message that lets the user know that feature isn’t supported. 

For example, the Weather skill supports checking the temperature and the forecast but can't check the air quality:

<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte0773407457c5067/634f6d961e79f1285f688603/shout.png" alt="User icon" style="vertical-align: middle; padding-right: 10px;">User: "_OK Webex, ask Weather to check the air quality_"<br>
<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte37071e600490842/634f6d96bbff0b3fd98e1caa/skill-icon.png" alt="Skill icon" style="vertical-align: middle; padding-right: 10px;">Weather skill: "_I’m not able to help with that just yet!_"

If you notice a pattern in the unsupported queries that your users are attempting, you can collect them into an intent and give a more specific error message. You can also remind the user what you’re able to help with if it’s relevant to their query. Taking the example of air quality with our Weather skill, you might choose to reply with something more specific like:

<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte0773407457c5067/634f6d961e79f1285f688603/shout.png" alt="User icon" style="vertical-align: middle; padding-right: 10px;">User: "_OK Webex, ask Weather to check the air quality_"<br>
<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte37071e600490842/634f6d96bbff0b3fd98e1caa/skill-icon.png" alt="Skill icon" style="vertical-align: middle; padding-right: 10px;">Weather skill: "_I’m not able to check the air quality, but I can tell you today’s forecast_"

**3. Unknown Entity**

_Issue_: The user asks for something your skill supports, but your skill can’t resolve the entity or there are no results for that entity.

When your skill isn’t able to resolve an entity, let the user know by repeating the entity in the error message (with automatic speech recognition errors, it can be helpful for the user to see the query) and let them know the skill didn’t find any results.

Sometimes when a skill is listening, it might capture background speech or the user’s request might transcribe imperfectly. Rather than ending the interaction, we recommend giving the user another opportunity to reply with the relevant information.

<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte0773407457c5067/634f6d961e79f1285f688603/shout.png" alt="User icon" style="vertical-align: middle; padding-right: 10px;">User: "_OK Webex, ask Weather to check the forecast_"<br>
<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte37071e600490842/634f6d96bbff0b3fd98e1caa/skill-icon.png" alt="Skill icon" style="vertical-align: middle; padding-right: 10px;">Weather skill: "_Where would you like me to check the weather?_"<br>
<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte0773407457c5067/634f6d961e79f1285f688603/shout.png" alt="User icon" style="vertical-align: middle; padding-right: 10px;">User: "_..._"<br>
<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte37071e600490842/634f6d96bbff0b3fd98e1caa/skill-icon.png" alt="Skill icon" style="vertical-align: middle; padding-right: 10px;">Weather skill: "_Hmmm, where should I check the weather?_"

For these multi-turn re-prompts, we recommend that you limit the number of re-prompts. We only allow Webex Assistant to re-prompt three times. This avoids cases where the assistant could get stuck in a re-prompt loop as it picks up background noise, or the case when the assistant isn't able to understand the user and we don’t want to continue to frustrate them. After exhausting the re-tries, we let users know that we weren’t able to understand them.

<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte37071e600490842/634f6d96bbff0b3fd98e1caa/skill-icon.png" alt="Skill icon" style="vertical-align: middle; padding-right: 10px;">Weather skill: "_Hmmm, I wasn’t able to understand how to help._"

### Other Error Handling Guidelines

Here are some best practices for wording error messages.

**1. Avoid Apologies**

There’s no need to apologize for not finding results or for not yet supporting a feature.

**2. Tell the User Why**

Make sure that your error message makes clear what went wrong. Let’s look at an example error message:

<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte0773407457c5067/634f6d961e79f1285f688603/shout.png" alt="User icon" style="vertical-align: middle">User: "_OK Webex, ask Weather what the temperature is here_"

&#10005;&nbsp;<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte37071e600490842/634f6d96bbff0b3fd98e1caa/skill-icon.png" alt="Skill icon" style="vertical-align: middle"> Weather skill: "_I’m unable to access the geography code for this device_"

This error message communicates that the skill can't access certain information, but it doesn't explain why this relates to the user's request. The user asked for the temperature, but we're telling them something about the device instead. The user might infer that the geography code is needed to check the temperature, but, ideally, we prefer to be as specific as possible.

Here’s a better way to phrase this error message:

<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte0773407457c5067/634f6d961e79f1285f688603/shout.png" alt="User icon" style="vertical-align: middle">User: "_OK Webex, ask Weather what the temperature is here_"

&#10003;&nbsp;<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte37071e600490842/634f6d96bbff0b3fd98e1caa/skill-icon.png" alt="Skill icon" style="vertical-align: middle">"Skill: _Hmmm, I’m not able to get the temperature because I’m not sure where you are._"

This response lets the user know the root cause of the issue and why the skill can't complete the request.

**3. Avoid Using “I” in Error Messages**

Avoid using “I" when your skill can't perform a request, specifically when your skill isn't the reason for the error. Removing “I" pronouns and using sentences with “there" for cases where the response is negative boosts the user's trust in your skill.

<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte0773407457c5067/634f6d961e79f1285f688603/shout.png" alt="User icon" style="vertical-align: middle">User: "_OK Webex, ask Weather to get the weather in Eventide_"

&#10005;&nbsp;<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte37071e600490842/634f6d96bbff0b3fd98e1caa/skill-icon.png" alt="Skill icon" style="vertical-align: middle"> Skill: "_I didn’t find weather information for Eventide_"

&#10003;&nbsp;<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte37071e600490842/634f6d96bbff0b3fd98e1caa/skill-icon.png" alt="Skill icon" style="vertical-align: middle">"Skill: _There isn’t any weather information for Eventide_"
