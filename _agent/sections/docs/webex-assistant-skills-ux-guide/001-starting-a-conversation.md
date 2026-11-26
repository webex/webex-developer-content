---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-assistant-skills-ux-guide
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Starting a Conversation
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

## Starting a Conversation

It's easy for users to switch between using **Webex Assistant** and a **Webex
Assistant Skill**. To use a skill, they'll just need to include the skill's name in their command. Let's take a closer at the differences.



> **Info**
>
> This document was last updated on September 2020.



### Starting a Conversation with Webex Assistant

Each time a user starts a conversation with Webex Assistant or a Webex Assistant Skill, they'll need to begin with a wake word. The wake word is a phrase that wakes the assistant from sleep mode, so it's ready to help. 

Webex Assistant's wake words are "**OK Webex**" and "**Hey Webex**" and aren't configurable.

Following the wake word, ask the assistant a question or tell the assistant what you need &mdash; that's called the query. For example:

<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte0773407457c5067/634f6d961e79f1285f688603/shout.png" alt="User icon" style="vertical-align: middle; padding-right: 10px;">User: _"OK Webex, what can you do?_"

### Starting a Conversation with Webex Assistant Skills

To use a Webex Assistant Skill, add a skill invocation phrase when beginning a conversation. The skill invocation phrase will always follow the wake word, and includes an invoke verb and the skill name. The invoke verbs aren't configurable, but you'll define your skill's name (take a look at [Naming your Skill](https://developer.webex.com/docs/webex-assistant-skills-ux-guide#naming-your-skill)] for more details). Conversations with your skill will always begin with the wake word and an invocation phrase, for example:

<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte0773407457c5067/634f6d961e79f1285f688603/shout.png" alt="User icon" style="vertical-align: middle; padding-right: 10px;">User: "_OK Webex, &lt;invoke verb&gt; &lt;SkillName&gt;_"

Webex Assistant Skills gives users two ways to interact with your skill: **Open a skill** or **Ask a skill**. When a user is new to using your skill opening it is a great way to explore how it works and learn about the skill's functionality. When first using your skill, users might not know what it can do. We've found that offering a way for users to be introduced and to play around with the skill improves their understanding, empowering them to become an advanced skill user. Once users are more familiar with your skill, they can use **ask a skill** to ask a question or tell it what they'd like it to do to. This works well for more advanced users who no longer need an introduction to your skill.

### Open a Skill

To open the skill, use either "open" or "talk to" as the invoke verb. Following the same pattern explain previously, a user would use a wake word, followed by an open invoke verb, and then the skill name.

<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte0773407457c5067/634f6d961e79f1285f688603/shout.png" alt="User icon" style="vertical-align: middle">User: "_OK Webex, open &lt;SkillName&gt;_"<br>
<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte0773407457c5067/634f6d961e79f1285f688603/shout.png" alt="User icon" style="vertical-align: middle">User: "_OK Webex, talk to &lt;SkillName&gt;_"

### Ask a Skill

To ask the skill a question, use "ask" or "tell" as the invoke verb. When users are asking a skill something, their query is included, too.

Open invoke verbs: "ask," "tell".

<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte0773407457c5067/634f6d961e79f1285f688603/shout.png" alt="User icon" style="vertical-align: middle">User: "_OK Webex, ask &lt;SkillName&gt; &lt;query&gt;_"<br>
<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte0773407457c5067/634f6d961e79f1285f688603/shout.png" alt="User icon" style="vertical-align: middle">User: "_OK Webex, tell &lt;SkillName&gt; &lt;query&gt;_"<br>

Remember: all conversations with your skill will begin with a wake word and a skill invocation phrase.
