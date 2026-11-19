---
type: Excerpt
canonical_url: https://developer.webex.com/docs/flow-orchestration
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Introduction
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/flow-orchestration). [Full Markdown](../../../../docs/flow-orchestration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md) [Restrictions](008-restrictions.md)

## Article introduction

Learn how to author a Webex Contact Center flow as a JSON document and import it through the Flow Orchestration APIs — entirely programmatically, without the UI.

## Selected section

## Introduction

A flow is a directed graph that describes the logical steps of a contact-center interaction. Each box on the canvas is a **node** that runs one **activity** — play a prompt, queue a contact, end the interaction — and the arrows between boxes are **edges** that decide which node runs next.

The Flow Orchestration APIs let you discover the activities and events available in your project, assemble those nodes and edges into a Flow JSON document, validate it, and import it as a draft on the tenant — the same headless `discover → assemble → validate → import` loop that AI-assisted flow authoring builds on.

A Flow document is made up of these pieces:

- **Start node** — the single entry point. It has `activityType: "start"` and `properties.activityName: "start"`. Its `properties.flowType` carries the trigger binding (`eventSourceName`, `eventClassificationName`, `eventSpecificationName`); for inbound telephony the `eventSpecificationName` is `ContactStartWorkflow`.
- **Action nodes** — the work the flow does. They have `activityType: "action"` and name the activity in `properties.activityName` (for example `play-message`).
- **End node** — terminates the interaction. It has `activityType: "end"`, for example `properties.activityName: "disconnect-contact"`.
- **Edges** — connect nodes and select which branch fires through the edge's `condition` (and, for a branching port, the edge's `properties`).
- **Variables** — named values the flow reads and writes.
- **Event flow** — a separate node/edge graph that runs when a bound event fires (this is how a global error handler is modeled).
- **Preferences** — flow-level settings.

Activity names, event names, and input fields are discovered per project at runtime — this guide uses the canonical values returned for a telephony project, but you should read the values for your own project from the discovery endpoints in [Before you begin](https://developer.webex.com/docs/flow-orchestration#before-you-begin).
