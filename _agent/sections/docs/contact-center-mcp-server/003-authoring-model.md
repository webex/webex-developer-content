---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-center-mcp-server
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Authoring Model
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-center-mcp-server). [Full Markdown](../../../../docs/contact-center-mcp-server.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication](005-authentication.md) [Scopes](006-scopes.md)

## Selected section

## Authoring Model

Use FlowV2 for flow create, read, save, patch, export, and validation workflows.

| Concept | How to use it |
|---------|---------------|
| FlowV2 | The flow authoring object. Top-level fields include schemaVersion, id, orgId, projectId, flowType, name, version, variables, nodes, edges, and eventFlows. |
| Nodes | Each node uses a unique name, a coarse activityType, and activity-specific properties. The specific activity is identified by properties.activityName. |
| Edges | Edges connect node names with from, to, and condition. Edge conditions should come from ActivityV2.outputPorts[].condition. |
| ActivityV2 | The activity discovery schema. Use `wxcc-get-activity-definitions` or `wxcc-describe-activity` before authoring activity nodes. |
| Choices | Use `wxcc-get-choices` for org-specific input values instead of guessing IDs or display names. |
