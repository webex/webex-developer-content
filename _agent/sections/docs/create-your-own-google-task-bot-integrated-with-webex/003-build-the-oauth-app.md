---
type: Excerpt
canonical_url: https://developer.webex.com/docs/create-your-own-google-task-bot-integrated-with-webex
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Build the OAuth App
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/create-your-own-google-task-bot-integrated-with-webex). [Full Markdown](../../../../docs/create-your-own-google-task-bot-integrated-with-webex.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](001-prerequisites.md)

## Article introduction

This article explains how you can create your own Webex-integrated Google Task bot.

## Selected section

## Build the OAuth App

To build the app:

1. Use the Google Tasks API to authenticate users and access their tasks.
1. Use the Webex Messages API to post task updates to a Webex space.
1. When a task is created or updated in Google Tasks, use the Webex API to send a message to the relevant Webex space.
