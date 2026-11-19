---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-custom-messaging-channel
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Attachment URL Requirements
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bring-your-own-custom-messaging-channel). [Full Markdown](../../../../docs/bring-your-own-custom-messaging-channel.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](003-before-you-begin.md) [Authentication For Custom Messaging Integrations](004-authentication-for-custom-messaging-integrations.md)

## Article introduction

Connect an external messaging channel to Webex Contact Center through middleware that uses the Custom Messaging APIs.

## Selected section

## Attachment URL Requirements

These requirements apply to middleware-provided attachment URLs used by:

- Create Task
- Task Messages
- Flow/system-sent Custom Messaging attachments where the platform must retrieve the file

Requirements:

- The attachment URL must use `https`
- The attachment URL must be retrievable by the platform
- File type is resolved from the URL extension when present
- If the URL has no usable extension, the platform uses the provided filename as the fallback
- If the effective file type is unsupported, the message is rejected
- File size must be determinable from remote metadata such as `Content-Length`
- If file size cannot be determined reliably, the message is rejected

These rules are separate from agent desktop attachment uploads, which follow a different UI-driven validation path.
