---
type: Excerpt
canonical_url: https://developer.webex.com/docs/admin-approval-guide-for-agentic-apps
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Security Review
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/admin-approval-guide-for-agentic-apps). [Full Markdown](../../../../docs/admin-approval-guide-for-agentic-apps.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Enablement Scope & Assignment](005-enablement-scope-assignment.md)

## Article introduction

---

This is a review guide for organization administrators evaluating and approving MCP Servers and A2A Agents before enabling them for organizational users. It provides guidelines to validate that an agentic app meets security, quality, and governance standards.

---

## Selected section

## Security Review

### Input Validation Posture

Verify the developer has implemented proper input handling:

| Check | Evidence to Look For |
|-------|---------------------|
| Schema enforcement | Strict JSON Schema with `additionalProperties: false` |
| Type safety | Explicit types (no untyped fields or `any`) |
| Length bounds | `maxLength` on string fields; `maximum`/`minimum` on numbers |
| Pattern validation | Regex patterns for structured strings (IDs, emails, URLs) |
| Enum constraints | Fixed value sets where applicable |
| No dynamic execution | No indication of `eval()`, template interpolation, or shell execution from input |

### Authorization & Least Privilege

| Check | What to Verify | Concern |
|-------|---------------|---------|
| Scope declaration | Every tool declares required scopes | Missing scopes → unclear access boundaries |
| Scope minimality | Scopes are narrowly defined per-tool | Broad scopes (`*`, `admin`) without justification |
| Your risk assessment matches behavior | Description and inputs are consistent with the impact you assessed | A tool that looks "low risk" but takes an unbounded `query` field that could exfiltrate data |
| Confused deputy prevention | User and server privileges are separated | Server might act with elevated access on behalf of regular users |
| Token handling | Short-lived, scoped tokens preferred | Long-lived tokens, broad audience claims |

### Data Handling & Privacy

| Check | What to Verify |
|-------|---------------|
| Data minimization | Tool only accesses/returns data needed for its function |
| PII handling | Personal data is identified and protected |
| Logging posture | Developer confirms no PII/secrets in logs |
| Encryption | Data encrypted in transit (TLS) and at rest |
| Retention | Clear retention policy with secure deletion |
| Cross-session isolation | No data leakage between users or sessions |
| Context limitations | Context size and lifetime are bounded |

### Network & Supply Chain

| Check | What to Verify |
|-------|---------------|
| HTTPS only | Server endpoint uses TLS (no HTTP fallback) |
| Certificate validity | Valid cert from trusted CA; not self-signed |
| Outbound restrictions | Server limits egress to necessary destinations |
| SSRF protection | Server blocks requests to internal/private addresses |
| Dependency posture | Dependencies are pinned and scanned |
| SBOM available | Software bill of materials provided on request |
| Build integrity | Signed builds or container images where applicable |

### Injection & Manipulation Defenses

| Risk | What to Check |
|------|--------------|
| Prompt injection | Tool descriptions don't contain instruction-like text that could manipulate LLMs |
| Tool poisoning | Metadata is factual, not suggestive or imperative |
| Name shadowing | Tool names don't duplicate well-known tools from other servers |
| Data-as-instructions | Outputs separate data from executable content |
| Command injection | No evidence of string concatenation for system commands |

---
