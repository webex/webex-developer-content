---
type: Excerpt
canonical_url: https://developer.webex.com/docs/best-practices-for-building-mcp-and-a2a-servers
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Designing Your Tools & Skills
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/best-practices-for-building-mcp-and-a2a-servers). [Full Markdown](../../../../docs/best-practices-for-building-mcp-and-a2a-servers.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

---

This is a guide for developers building MCP Servers and A2A Agents for the Webex ecosystem. Following these practices helps your server be secure, reliable, and performant while delivering a consistent experience for AI agents and end users.

---

## Selected section

## Designing Your Tools & Skills

### Granularity

Pick the right level of abstraction for each tool or skill. The goal is to present **cognitively meaningful, single-goal actions** that an AI agent can reliably select and use.

**Do:**
- Compose multiple low-level steps into a single "do-the-thing" tool where feasible
- Keep your total tool count manageable — many agentic clients enforce tool count limits
- Think in terms of user intent, not API coverage

**Don't:**
- Mirror every low-level REST API as a separate tool
- Create tools so coarse they become ambiguous or unusable
- Create tools so fine-grained they overwhelm the model's planning capacity

**Example:**

| Approach | Tools | Verdict |
|----------|-------|---------|
| Fine-grained (bad) | `list_users`, `list_events`, `create_event` | Too many steps; forces LLM to plan multi-call sequences |
| Right granularity (good) | `schedule_event` (finds free time + creates event) | Single intent; composable internally |



> **Tip**
>
> Start coarse, then break apart only when evaluation shows LLMs need more granular control for specific use cases.



---

### Naming Conventions

Names are the primary signal AI agents use to select tools. Make them **descriptive, stable, and unambiguous**.

**Rules:**

| Rule | Guidance |
|------|----------|
| Format | Use `domain.entity.verb` pattern (e.g., `documents.reports.export`, `records.search`) |
| Length | Keep names ≤ 60 characters for broadest client compatibility |
| Stability | Never rename a published tool — it breaks existing references and admin configurations |
| Uniqueness | Names must not collide with tools from other servers; use domain prefixes to prevent shadowing |
| Character set | Alphanumeric, dots, underscores, hyphens only — avoid spaces and special characters |

**Avoid:**
- Generic names like `run`, `execute`, `do_action`
- Imperative/suggestive language in descriptions that could manipulate LLM behavior
- Names that duplicate or shadow tools from other servers

---

### Input & Output Schemas

Define **precise JSON Schemas** for all tool inputs and outputs. These schemas serve dual purposes: runtime validation and LLM tool selection.

#### Input Schema Best Practices

- Use explicit types, bounds, regex constraints, enumerations, and max sizes
- Mark required vs. optional fields clearly
- Provide `description` for each field — this helps LLMs populate arguments correctly
- Avoid free-form string inputs where structured alternatives exist
- Reject unknown/extra fields at runtime

```json
{
  "type": "object",
  "required": ["document_id", "format"],
  "properties": {
    "document_id": {
      "type": "string",
      "pattern": "^[a-f0-9]{32}$",
      "description": "The unique 32-character hex document identifier"
    },
    "format": {
      "type": "string",
      "enum": ["pdf", "csv", "txt"],
      "description": "Export format for the report"
    },
    "include_metadata": {
      "type": "boolean",
      "default": true,
      "description": "Whether to include metadata in the export"
    }
  },
  "additionalProperties": false
}
```

#### Output Schema Best Practices

Keep outputs **concise** to reduce token usage and cognitive load. Structure outputs with clear separation between user-facing and LLM-facing content.

**User-facing content** — natural language, friendly for display:
```json
{
  "summary": "Your report has been exported successfully.",
  "status_badge": { "label": "Complete", "variant": "success" },
  "help_links": [
    { "label": "View report", "href": "https://example.com/reports/abc123" }
  ]
}
```

**LLM-facing content** — structured, unambiguous, machine-optimized:
```json
{
  "canonical_facts": {
    "document_id": "a1b2c3d4e5f6...",
    "export_format": "pdf",
    "file_size_bytes": 245000,
    "page_count": 12
  },
  "reasoning_hints": [
    "If user asks to share, use the download_url.",
    "Convert timestamps to user's timezone before display."
  ],
  "guardrails": {
    "redact_fields_in_user_facing": ["document_id"],
    "max_tokens_user_summary": 80
  }
}
```



> **Key Principle**
>
> User-facing content should be natural and friendly. LLM-facing content should be structured with unambiguous field names, canonical facts, and explicit guardrails.



---

### Resources vs. Tools

MCP supports both Resources and Tools. Choose the right primitive for each capability.

| Use Resources when... | Use Tools when... |
|----------------------|-------------------|
| Data is read-only and browsable | Action has side effects |
| Content is large (documents, lists, knowledge bases) | LLM needs direct invocation control |
| Data is fetched on-demand by the client | You need the same capability over MCP **and** A2A |
| You want to reduce tool count and context bloat | Data is dynamic and requires parameters |



> **Note**
>
> A2A does not have a flexible resource abstraction like MCP. If you need dual-protocol exposure for the same data, model it as a tool/skill.



**Resource guidelines:**
- Use typed URIs with clear schemes (e.g., `https://example.com/documents/{id}/report`)
- Declare MIME types explicitly
- Keep resources stateless and cacheable where possible

---
