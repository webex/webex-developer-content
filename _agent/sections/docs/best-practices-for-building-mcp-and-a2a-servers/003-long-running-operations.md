---
type: Excerpt
canonical_url: https://developer.webex.com/docs/best-practices-for-building-mcp-and-a2a-servers
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Long-Running Operations
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/best-practices-for-building-mcp-and-a2a-servers). [Full Markdown](../../../../docs/best-practices-for-building-mcp-and-a2a-servers.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

---

This is a guide for developers building MCP Servers and A2A Agents for the Webex ecosystem. Following these practices helps your server be secure, reliable, and performant while delivering a consistent experience for AI agents and end users.

---

## Selected section

## Long-Running Operations

For any operation that may exceed a few seconds, implement proper progress reporting and resumability.

### Progress & Status Reporting

- **Stream progress early and often** — don't leave the client waiting without feedback
- Send status updates as SSE events or gRPC stream messages
- Include both machine-readable status and human-friendly messages
- Support `Last-Event-ID` header for reconnection after connection drops
- Buffer recent events for several minutes to enable resume

**Example progress message:**
```json
{
  "type": "progress",
  "percent": 45,
  "message": "Processing report sections (3 of 7)...",
  "estimatedRemainingSeconds": 30
}
```

### Elicitation (Human-in-the-Loop)

Use elicitation when inputs are missing, ambiguous, or when explicit approval is required for sensitive actions.

**Guidelines:**
- Specify all elicitation fields in your tool specification — admins review these during approval
- Use form-based elicitation for structured input collection
- Provide clear, user-friendly prompts explaining what is needed and why
- Set reasonable timeouts for elicitation responses
- Design for the case where elicitation is denied or times out

**When to require elicitation:**
- Destructive operations (delete, overwrite)
- Operations involving financial transactions or external system changes
- Actions where confidence or impact thresholds are exceeded
- Access to sensitive data beyond the tool's normal scope

### Delegation & Sampling

Delegation allows your server to pause execution and request a sub-task from another agent or the client's LLM.

**Guidelines:**
- Keep bounded timeouts for delegated tasks
- Define a clear schema for expected sub-results
- Implement recovery logic for timeout and failure scenarios
- For MCP sampling: useful when your server lacks an LLM or when user context must stay client-side
- Avoid circular delegation chains

### Operation Artifacts

When outputs are too large to stream directly:
- Store as files and return typed URIs with metadata
- Use **signed URLs** with limited validity (not permanent public URLs)
- Include MIME type, file size, and creation timestamp in metadata
- Define lifecycle/retention policies for stored artifacts
- Examples: CSV exports, PDF reports, log files, evidence bundles

---
