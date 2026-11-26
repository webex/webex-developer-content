---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-center-operation-mcp-server-beta
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- 3. Run basic read-only checks
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-center-operation-mcp-server-beta). [Full Markdown](../../../../docs/contact-center-operation-mcp-server-beta.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Use this guide to test the Webex Contact Center Operation MCP Server with a supported MCP client during the Webex Developer Beta. For the complete tool reference, see [Contact Center Operation MCP Server](https://developer.webex.com/docs/contact-center-operation-mcp-server).

## Selected section

## 3. Run basic read-only checks

Run these checks first using a known test organization and, where possible, a known test object.

| Check | Operations MCP tool | What to do | Expected result |
|---|---|---|---|
| Organization overview | `wxcc-operations-describe-org` | Ask for a high-level Contact Center overview. | The response describes only the authorized organization and clearly labels counts or samples. |
| Metric discovery | `wxcc-operations-describe-metrics` | Ask which fields and metrics are available for a report. | The response identifies supported fields instead of guessing. |
| Schema check | `wxcc-operations-validate-schema` | Run when a report or Search query may be affected by a field or schema issue. | The result clearly says whether validation succeeded, found a difference, or could not complete. |
| Configuration list | `wxcc-operations-list-config` | List one approved resource such as a queue, team, site, entry point, skill, or user. | Only authorized configuration is returned. |
| Configuration detail | `wxcc-operations-get-config-object` | Retrieve one known object by ID. | The requested object is returned without changing it. |
| Configuration references | `wxcc-operations-get-configuration-references` | Find objects that refer to one known configuration object. | References are limited to the authorized organization and clearly identified. |

### Basic pass criteria

- The response contains only authorized organization data.
- Counts, returned rows, and any limits are explained clearly.
- A missing object is not reported as definitively absent when the search was incomplete.
- No configuration changes occur.
- The client identifies the tool used or makes the result traceable to the test.
