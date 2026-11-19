---
type: Excerpt
canonical_url: https://developer.webex.com/docs/cc-web-widgets-components-realtimetranscript
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Configuration Notes
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/cc-web-widgets-components-realtimetranscript). [Full Markdown](../../../../docs/cc-web-widgets-components-realtimetranscript.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The `RealTimeTranscript` component renders the live voice transcript for the currently selected task.

## Selected section

## Configuration Notes

- Use this widget together with task-selection widgets such as `IncomingTask` or `TaskList`, so the store has a current task to bind to.
- Real-time transcription data is available only when the Contact Center configuration enables the underlying transcript feature for the agent.
- This widget is intended for live voice interactions. If no transcript is available, it renders an empty-state message.
