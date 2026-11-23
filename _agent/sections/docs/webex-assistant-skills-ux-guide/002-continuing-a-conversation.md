---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-assistant-skills-ux-guide
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Continuing a Conversation
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

## Continuing a Conversation

After starting a conversation with your Webex Assistant Skill, the assistant can be in "listening" or "not listening" mode. When the assistant is listening, the user can keep speaking without having to use a wake word or an invocation phrase to talk with your skill. When the assistant isn't listening, the user will need to use a wake word and invocation phrase to continue using your skill. The Webex Assistant icon indicates if the assistant is listening.

When the assistant is listening, you'll see the icon below. When you see this icon, you can keep talking:

![Listening mode](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltc123f0f2a3c7e580/634f2548885d1d218e487c14/listening-mode.png)

When the assistant isn't listening, you'll see the icon below. When you see this icon, use a wake word and invocation phrase to keep using your Webex Assistant Skill:

![Not listening mode](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt2203bf30cb22c942/634f258c1e79f1285f688594/not-listening.png)

Let's look at some conversations with our example skill, the Weather skill, to better understand what interacting with "listening" and "not listening" modes look like.

In the following conversation, the Weather skill keeps listening:

<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte0773407457c5067/634f6d961e79f1285f688603/shout.png" alt="User icon" style="vertical-align: middle; padding-right: 10px;">User: "_OK Webex, ask weather_"<br>
<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte37071e600490842/634f6d96bbff0b3fd98e1caa/skill-icon.png" alt="Skill icon" style="vertical-align: middle; padding-right: 10px;">Weather skill: "_Where should I check the weather?_"<br>
<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte0773407457c5067/634f6d961e79f1285f688603/shout.png" alt="User icon" style="vertical-align: middle; padding-right: 10px;">User: _"San Francisco"_<br>
<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte37071e600490842/634f6d96bbff0b3fd98e1caa/skill-icon.png" alt="Skill icon" style="vertical-align: middle; padding-right: 10px;">Weather skill: "_It's 68° and partly cloudy in San Francisco today._"<br>

When the skill asks a question it's in listening mode because it's waiting for the user to provide more information. After the skill finishes the user's request &mdash; in this case, telling them the weather in San Francisco &mdash; it stops listening. The user's request has been fulfilled, and the conversation ends. If the user wanted to ask the Weather skill for the forecast somewhere else, they would need to start a new conversation using a wake word and skill invocation phrase. 

In the conversation below, the skill doesn't keep listening. The skill has completed the user's request, and the conversation ends:

<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte0773407457c5067/634f6d961e79f1285f688603/shout.png" alt="User icon" style="vertical-align: middle; padding-right: 10px;">User: "OK Webex, ask Weather to check the weather in San Francisco for me"<br>
<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte37071e600490842/634f6d96bbff0b3fd98e1caa/skill-icon.png" alt="Skill icon" style="vertical-align: middle; padding-right: 10px;">Weather skill: "It's 68° and partly cloudy in San Francisco today._"<br>
