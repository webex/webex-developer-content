---
type: Excerpt
canonical_url: https://developer.webex.com/docs/migrating-to-cc-vcon-transcripts
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Compatibility recommendation
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/migrating-to-cc-vcon-transcripts). [Full Markdown](../../../../docs/migrating-to-cc-vcon-transcripts.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This guide explains how to migrate API consumers from Legacy Voice Transcript Format to Voice vCon Transcript Format. The legacy transcript format represents only the Human Agent to customer leg of a conversation. The Voice vCon transcript format can represent the full Contact Center conversation, including AI Agents, Human Agents, and customers in the same interaction.

---

The legacy format stores transcript output as speech recognition results under `responseContents`. The Voice vCon format stores the conversation as a vCon-style document with top-level conversation metadata, participants, and dialog entries. For the complete object model, refer to the [vCon Conversation Data Container draft (revision 04)](https://datatracker.ietf.org/doc/html/draft-ietf-vcon-vcon-core-04).

## Selected section

## Compatibility recommendation

For the safest rollout, support both formats during the migration window and update downstream consumers to read the Voice vCon transcript fields directly. Once all stored transcripts and API responses use the Voice vCon format, remove the legacy parser and any dependencies on confidence scores, recognition alternatives, and word-level offsets.
