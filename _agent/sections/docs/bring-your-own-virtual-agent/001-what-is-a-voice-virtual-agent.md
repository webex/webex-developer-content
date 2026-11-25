---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-virtual-agent
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- What is a Voice Virtual Agent?
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bring-your-own-virtual-agent). [Full Markdown](../../../../docs/bring-your-own-virtual-agent.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Phase 2 - Authentication](003-phase-2-authentication.md)

## Article introduction

As part of the "Bring Your Own" (BYO) initiative, Webex Contact Center aims to enable seamless integrations with third-party AI providers, enhancing the Webex customer experience with cutting-edge AI innovations. Bring your own Virtual Agent is the first slice of all other other AI functionalities you can bring to Webex Contact Center product offerings.

## Selected section

## What is a Voice Virtual Agent?

In essence, a Voice Virtual Agent interacts with callers during voice calls and performs the following key functions:

1. Transcribes the caller's **speech to text** for AI processing.
1. Utilizes **Natural Language Understanding** to identify the caller's intent.
1. Maps the identified **intent** to an existing workflow (OR) uses **Generative AI** to create a text response.
1. Converts the generated **text to speech** which is then prompted to the caller back.
1. For escalated calls, provides the human agent with context by supplying the Virtual Agent's transcript or a summary.

![VA-flow](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt9c003e4b8bcb5ef8/6914d59ca6e2a9fd57b7ea60/VACallFlowWithEscalation.jpg?branch=integration)

*Fig 1: A sample Virtual agent call that is escalated to a human agent*
