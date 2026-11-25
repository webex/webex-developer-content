---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-custom-messaging-channel
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
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

- Supply the attachment URL in the JSON key `url`; it must use `https` and be at most 2,000 characters long
- The service must be able to download the file directly, without a separate login or Authorization header. A signed or short-lived URL is acceptable if it remains valid until the file is downloaded
- Supply a nonempty `fileName`. `mimeType` is optional; omitting it does not bypass file-type or content validation
- File-type validation uses the URL extension when present. If no usable extension is present, it can use the filename and content type returned by the file server, together with the supplied MIME type when applicable
- If the effective file type is unsupported by the configured channel policy, the message is rejected
- When the configured policy enforces attachment size limits, file size must be determinable from remote metadata such as `Content-Length`; otherwise, the message is rejected

These rules are separate from agent desktop attachment uploads, which follow a different UI-driven validation path.
