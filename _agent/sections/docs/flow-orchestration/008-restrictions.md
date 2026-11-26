---
type: Excerpt
canonical_url: https://developer.webex.com/docs/flow-orchestration
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Restrictions
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/flow-orchestration). [Full Markdown](../../../../docs/flow-orchestration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md)

## Article introduction

Learn how to author a Webex Contact Center flow as a JSON document and import it through the Flow Orchestration APIs — entirely programmatically, without the UI.

## Selected section

## Restrictions

1. A flow's main process must contain exactly one start node (`activityType: "start"`). A document without one is rejected by both `:validate` (`valid: false`) and `:import` (`400`).
2. A flow `name` must be unique within the project unless you import with `overwrite=true`; otherwise import returns `409 Conflict`.
3. `:validate` and `:import` do not enforce identical rules — passing `:validate` does not guarantee `:import` will succeed, and `:validate` may reject a document (for example an invalid edge `condition`) that `:import` still accepts.
4. Node `name` values and edge `id` values must be unique within their process, and an edge may only reference nodes in the same process (no edges between the main flow and the event flow).
5. When patching a draft, edges that reference a removed node must be removed in the same patch, or the merged document fails validation.
6. A custom function `name` must be unique within the organization; a duplicate name returns `409 Conflict`.
7. Save and patch requests that pass `expectedVersion` fail with `409 Conflict` if the server-side draft version has moved on.
8. The Flow Orchestration API does not expose a delete operation for flows — an imported flow persists as tenant state. In shared or test tenants, prefix flow names (for example `WXCC_TEST_`) so they are easy to identify, and remove them through Control Hub when you are done.
