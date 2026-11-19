---
type: Excerpt
canonical_url: https://developer.webex.com/docs/flow-orchestration
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Recommendations and best practices
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/flow-orchestration). [Full Markdown](../../../../docs/flow-orchestration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md) [Restrictions](008-restrictions.md)

## Article introduction

Learn how to author a Webex Contact Center flow as a JSON document and import it through the Flow Orchestration APIs — entirely programmatically, without the UI.

## Selected section

## Recommendations and best practices

- Discover before you author. List activities with `listActivityDefinitions` and events with `listEventSpecifications`, and use the returned `activityName` values and event `name`s verbatim rather than hard-coding them or assuming a naming convention — the discovery responses are self-describing.
- Validate before importing, but treat a successful `:validate` as necessary, not sufficient; always handle a possible `422` on `:import`.
- Resolve constrained inputs (queues, audio files, teams) with `getActivityInputChoices` instead of guessing values, to avoid `UNKNOWN_*` validation errors.
- Use `PATCH` for incremental edits, and pass `expectedVersion` to enable optimistic locking when multiple editors or automations touch the same draft.
- Surface the validation `message` (and `suggestion` when present) to the author; the error shape does not always include a stable machine-readable `code`, so don't rely on one for control flow.
- For custom functions, test (`:test`) before publishing, and publish under explicit tags (`Dev`/`Test`/`Latest`/`Live`) so versions stay addressable.
- Keep sensitive values in `isSecure` variables so they are masked in logs and reports.
