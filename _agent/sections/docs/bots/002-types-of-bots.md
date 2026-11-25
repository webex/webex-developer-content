---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bots
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Types of Bots
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bots). [Full Markdown](../../../../docs/bots.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Give Webex users access to outside services right from their Webex spaces. Bots help users automate tasks, bring external content into the discussion, and gain efficiencies.

[Create a Bot](<https://developer.webex.com/my-apps/new/bot>)

## Selected section

## Types of Bots

Bots come in all different shapes and sizes. Here are some ideas for a few different types of bots you can make:

### Notifiers

Notifier bots typically respond to events in external services and post a summary in Webex. For example, a _GitHub Bot_ may listen for commits on a particular repo and post the committer's name and comment into a Webex space set aside for this purpose. Or a _Deal Bot_ that lives in an account-specific space and posts updates from a CRM along with relevant news about the company like a product launch or earnings report.

### Controllers

Controller bots act as a text-based remote control for external services. For example, a _Jira Bot_ may allow software engineers and product managers to control or query information from the popular bug tracking system Jira, all from the comfort of a Webex space.

<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt15175555e3f933b0/5d4ad4ec0331293861b7a626/Bot-Example.png" width="500" height="245" title="Controller Bot"></img>

Controller bots are generally passive, waiting for someone in the room to issue a command. In group rooms, bots can only see messages in which they are mentioned (1:1 rooms bots can see all messages as they are automatically "mentioned"). Your users are required to mention the bot preceding the command like `@jira find WEBSITE-22` where `@jira` is the bot's name.

Currently, the Webex SDKs do not support extracting commands from messages. You'll need to parse it out after the mention. Future versions of the Webex SDKs will have built-in support for commands. Keep your eyes on the blog for updates.

### Assistants

Virtual assistants are the holy grail of chatbots. At minimum, an assistant should understand natural language, allowing the user to ask it questions as they would to a human.

Recent advancements in NLP (Natural Language Processing) have made understanding natural language requests not only possible, but quite accessible to the average developer. Most notably, Google launched [Google Cloud Natural Language API](https://cloud.google.com/natural-language/) in the summer of 2016, providing syntax parsing, sentiment analysis and deep noun classification.

Responding to natural language is a good first step but a truly exceptional assistant bot will be conversational, using past interactions to contextualize the most recent query. This is a very complex problem domain; luckily there are companies like [Dialogflow](https://dialogflow.com/) providing a conversational platform built specifically for bots.
