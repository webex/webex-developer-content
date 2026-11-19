---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-assistant-skills-guide
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Skills, Simple Skills and MindMeld Skills
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-assistant-skills-guide). [Full Markdown](../../../../docs/webex-assistant-skills-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Requirements](002-requirements.md)

## Article introduction

The [Webex Assistant Skills SDK](https://github.com/cisco/webex-assistant-sdk) is designed to simplify the process of creating a Webex Assistant skill.

---



> **Warning**
>
> No new features are being added to Webex Assistant Skills and only skills added through May 2025 are directly supported by Cisco.

## Selected section

## Skills, Simple Skills and MindMeld Skills

A skill is a web service that takes a request containing some text and some context, analyzes that information and responds accordingly. The level of analysis depends on the tasks the skill wishes to accomplish. Some skills require only looking for keywords in the text, while others may require performing Natural Language Processing in order to handle more complex conversational flows from the user.

This SDK has tooling for creating two types of skills: **simple skills** and **MindMeld skills**. These should serve as templates for basic and conversational skills. Let's now take a look at these templates in detail.

### Simple Skills

**Simple skills** do not perform any type of Machine Learning or Natural Language Processing analysis on the requests. These skills are a good starting point for developers to start tinkering. Most developers would start with a **simple skill** and then migrate to a **MindMeld skill**, or incorporate a different NLP tool. 

Imagine a skill whose only task is to turn on and off the lights in the office. Some typical queries could be:

- "Turn on the lights"
- "Turn off the lights"
- "Turn on the lights please"
- "Turn the lights off"

In this particular case, we can look for the words **on** and **off** in the received text. If **on** is present, the skill turns on the lights and responds accordingly, and similarly for the **off** intent.

A simple regex suffices for this use case. Simple skills in the SDK do this: they provide a template where you can specify the regexes you care about, and have them map to specific handlers (**turn_on_lights** and **turn_off_lights** in our example).

We'll build a simple skill in [this section](https://developer.webex.com/docs/webex-assistant-skills-guide#building-a-simple-skill)  

### MindMeld Skills

[MindMeld](https://mindmeld.com/) is an open source natural language processing (NLP) library made available by Cisco.
This library makes it easy to perform NLP on any text query and identify intents and entities in an actor's requests. Using this library, you can handle more complex and nuanced queries from users. More information on the MindMeld library can be found on the project's [Learn More](https://www.mindmeld.com/docs/index.html) page. 

Let's take the case of a skill for ordering food. Queries might look like the following:

- "Order a pepperoni pizza from Super Pizzas."
- "Order a pad thai from Thailand Cafe for pickup in an 1 hour."
- "I want a hamburger with fries and soda from Hyper Burgers."

As we can see, using regexes for these cases can get out of hand. We would need to be able to recognize every single dish from every single restaurant, which might account for hundreds or thousands of regexes. As we add more dishes and restaurants, updating the codebase becomes a real problem.

To simplify leveraging MindMeld, the SDK has built in support for adding in the NLP functionality to your skill. These
**MindMeld skills** can then perform NLP analysis on the requests. This type of skill is a good template for cases where the queries may have a lot of variation. For the example above, once you've created your **MindMeld skill**, the skill will be able to identify entities like **dishes**, **restaurants**, **quantities**, and **times**. This makes performing the required actions an easier job.

We'll build a MindMeld skill in [this section](https://developer.webex.com/docs/webex-assistant-skills-guide#building-a-mindmeld-skill)
