---
type: Excerpt
canonical_url: https://developer.webex.com/docs/agentic-apps-overview
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- What is Schema?
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/agentic-apps-overview). [Full Markdown](../../../../docs/agentic-apps-overview.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Learn the key concepts, terminology, and components of agentic apps and the Model Context Protocol (MCP) for building AI-powered integrations.

---

This guide introduces the foundational concepts behind agentic apps and the Model Context Protocol (MCP), including key terminology, server capabilities, and schema definitions.

## Selected section

## What is Schema?

**Schema** - A formal description of the structure, data types, and constraints of information exchanged between an MCP server and client.

**Input Schema** - Defines the required and optional arguments a tool accepts, enabling the agent to construct valid tool calls. Ensures type safety and argument validation.

**Output Schema** - Describes the expected structure of data returned by a tool, allowing the agent to parse and act on tool results predictably.

**Annotations** - Metadata fields attached to tools or schemas that extend functionality beyond standard schema defined by MCP or A2A protocol. They can include UI hints, privacy indicators, categorization tags, or execution constraints.
