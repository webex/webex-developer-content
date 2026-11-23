---
type: Excerpt
canonical_url: https://developer.webex.com/docs/create-your-own-gmail-bot-integrated-with-webex
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Build the OAuth App
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/create-your-own-gmail-bot-integrated-with-webex). [Full Markdown](../../../../docs/create-your-own-gmail-bot-integrated-with-webex.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](001-prerequisites.md)

## Article introduction

This article explains how you can create your own Webex-integrated Google Gmail bot.

## Selected section

## Build the OAuth App

To build the OAuth app:

1. Use the Gmail API to authenticate users and access their emails.
1. Use the Webex Messages API to post email notifications to a Webex space.
1. When a new email is received, use the Webex API to send a notification message to the relevant Webex space.
1. Implement functionalities for replying to emails, marking as starred, saving drafts, and deleting emails using the Gmail API.
