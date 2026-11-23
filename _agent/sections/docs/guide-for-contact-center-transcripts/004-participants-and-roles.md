---
type: Excerpt
canonical_url: https://developer.webex.com/docs/guide-for-contact-center-transcripts
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Participants and Roles
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/guide-for-contact-center-transcripts). [Full Markdown](../../../../docs/guide-for-contact-center-transcripts.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Known Limitations](007-known-limitations.md)

## Article introduction

This guide explains how to find and parse Voice vCon transcript JSON returned through the Captures API. It focuses on the transcript file format; use the [Captures API reference](https://developer.webex.com/webex-contact-center/docs/api/v1/captures/list-captures) for endpoint details, authorization, request fields, limits, and the full response schema.

---

Voice vCon transcripts may contain conversations between:

- an AI Agent and a user
- a Human Agent and a user
- multiple AI Agents, Human Agents, and a user

The transcript file uses the `vcon` schema, which is based on the [vCon Conversation Data Container draft (revision 04)](https://datatracker.ietf.org/doc/html/draft-ietf-vcon-vcon-core-04). In this format, participants are represented in the top-level `parties` array and transcript messages are represented in the top-level `dialog` array.

## Selected section

## Participants and Roles

Participants in a Voice vCon transcript are listed in `parties`, following the vCon [party object](https://datatracker.ietf.org/doc/html/draft-ietf-vcon-vcon-core-04#section-4.2) model. Each dialog entry identifies its speaker through the `originator` index.

For example:

```json
{
  "parties": [
    {
      "role": "customer"
    },
    {
      "uuid": "69e23483c39ab81f25fa9bc8",
      "role": "virtual-agent"
    },
    {
      "uuid": "4f854080-9497-4b3d-aa4f-a406d0d6f8bd",
      "role": "agent"
    }
  ]
}
```

Allowed participant roles:

| Role | Description |
| --- | --- |
| `customer` | The end user or caller. |
| `virtual-agent` | The AI Agent participating in the conversation. |
| `agent` | The Human Agent participating in the conversation. |

Possible transcript participant combinations:

| Conversation type | Example roles in `parties` |
| --- | --- |
| AI Agent and user | `customer`, `virtual-agent` |
| Human Agent and user | `customer`, `agent` |
| AI Agent, Human Agent, and user | `customer`, `virtual-agent`, `agent` |

Do not assume a fixed party index for a role. Always resolve the speaker by reading:

```python
party = transcript["parties"][dialog_entry["originator"]]
```
