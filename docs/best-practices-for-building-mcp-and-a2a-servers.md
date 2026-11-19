---
type: Guide
title: Security Guides | Best Practices for Building MCP and A2A Servers
display_title: Best Practices for Building MCP and A2A Servers
canonical_url: https://developer.webex.com/docs/best-practices-for-building-mcp-and-a2a-servers
content_type: documentation
product_group:
- webex-suite
- webex-contact-center
categories:
- mcp
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/best-practices-for-building-mcp-and-a2a-servers)

---

This is a guide for developers building MCP Servers and A2A Agents for the Webex ecosystem. Following these practices helps your server be secure, reliable, and performant while delivering a consistent experience for AI agents and end users.

---

## Table of Contents

- [Designing Your Tools & Skills](#designing-your-tools--skills)
  - [Granularity](#granularity)
  - [Naming Conventions](#naming-conventions)
  - [Input & Output Schemas](#input--output-schemas)
  - [Resources vs. Tools](#resources-vs-tools)
- [Long-Running Operations](#long-running-operations)
  - [Progress & Status Reporting](#progress--status-reporting)
  - [Elicitation (Human-in-the-Loop)](#elicitation-human-in-the-loop)
  - [Delegation & Sampling](#delegation--sampling)
  - [Operation Artifacts](#operation-artifacts)
- [Security & Privacy](#security--privacy)
  - [Input Validation & Sanitization](#input-validation--sanitization)
  - [Authorization & Scopes](#authorization--scopes)
  - [Secrets Management](#secrets-management)
  - [Data Handling & Privacy](#data-handling--privacy)
  - [Supply Chain Security](#supply-chain-security)
  - [Network Security](#network-security)
  - [Injection & Manipulation Defenses](#injection--manipulation-defenses)
- [Reliability & Fault Tolerance](#reliability--fault-tolerance)
  - [Idempotency & Safe Retries](#idempotency--safe-retries)
  - [Scaling & Failover](#scaling--failover)
  - [Timeouts, Retries & Backoff](#timeouts-retries--backoff)
  - [Streaming & Reconnection](#streaming--reconnection)
- [Observability & Governance](#observability--governance)
  - [Structured Logging](#structured-logging)
  - [Metrics & SLOs](#metrics--slos)
  - [Audit Trails](#audit-trails)
  - [Versioning & Deprecation](#versioning--deprecation)
- [Testing & Evaluation](#testing--evaluation)
- [Production Readiness Checklist](#production-readiness-checklist)

---

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

## Security & Privacy

### Input Validation & Sanitization

Treat **all external input as untrusted** — whether from users, LLMs, or other agents.

**Mandatory practices:**

| Practice | Details |
|----------|---------|
| Schema validation | Validate all inputs against published JSON Schema before processing |
| Encoding normalization | Normalize Unicode, reject ambiguous encodings, enforce UTF-8 |
| Length limits | Enforce maximum lengths on all string fields |
| Character filtering | Block dangerous characters/patterns based on processing context |
| Parameterized execution | Use safe APIs for SQL, shell, templates — never concatenate strings |
| No dynamic evaluation | Disable `eval()`, unsafe deserialization, and runtime code generation |
| Output encoding | Encode/escape outputs per downstream sink context |
| File handling | Verify MIME types, reject zip-slip paths, guard against decompression bombs |
| Content-type enforcement | Validate `Content-Type` headers match actual payload |

**Context-specific sanitization:**

| Context | Sanitization |
|---------|-------------|
| SQL queries | Parameterized queries only; never interpolate |
| Shell commands | Allowlisted commands with typed parameters; no shell expansion |
| URL construction | Validate scheme, host; encode path/query; block `javascript:` and internal addresses |
| HTML/Markdown output | Escape or sanitize to prevent XSS injection |
| File paths | Normalize, reject traversal (`../`), use allowlisted directories |

### Authorization & Scopes

- Specify **every required scope** in your tool specification
- Enforce **least privilege** — request only minimum scopes needed
- Validate requested actions against granted scopes on every call (deny by default)
- Prevent confused-deputy scenarios by separating user and server privileges
- Propagate effective principals explicitly — don't assume inherited permissions

#### OAuth Server Metadata Discovery (RFC 8414)

If your server uses either OAuth auth type (`OAuth2_clientCredentials` or `OAuth2_authorizationCode`), expose a discovery endpoint at:

```text
https://<your-server-host>/.well-known/oauth-authorization-server
```

following [RFC 8414](https://datatracker.ietf.org/doc/html/rfc8414). When this endpoint is reachable, Webex auto-prefills the OAuth configuration during admin enablement, removing manual data-entry errors and enabling zero-touch setup for org admins.

**Minimum fields to publish:**

| Field | Purpose |
|-------|---------|
| `issuer` | The authorization server's identifier (URL) |
| `authorization_endpoint` | OAuth2 authorization endpoint (required for `OAuth2_authorizationCode`) |
| `token_endpoint` | OAuth2 token endpoint |
| `scopes_supported` | List of scope strings the admin can grant |
| `response_types_supported` | E.g., `["code"]` for authorization code flow |
| `grant_types_supported` | E.g., `["authorization_code", "client_credentials"]` |
| `token_endpoint_auth_methods_supported` | E.g., `["client_secret_basic", "client_secret_post"]` |
| `code_challenge_methods_supported` | E.g., `["S256"]` if you support PKCE |
| `registration_endpoint` | Optional — dynamic client registration endpoint, if supported |

**Example response:**

```json
{
  "issuer": "https://auth.example.com",
  "authorization_endpoint": "https://auth.example.com/oauth2/authorize",
  "token_endpoint": "https://auth.example.com/oauth2/token",
  "scopes_supported": ["read:documents", "write:documents", "read:reports"],
  "response_types_supported": ["code"],
  "grant_types_supported": ["authorization_code", "client_credentials"],
  "token_endpoint_auth_methods_supported": ["client_secret_basic", "client_secret_post"],
  "code_challenge_methods_supported": ["S256"]
}
```

**Implementation guidance:**
- Serve the endpoint over HTTPS with a valid TLS certificate
- Make it publicly reachable — no auth required to read it
- Return `Content-Type: application/json`
- Cache headers may be set to several hours; the document changes rarely
- If your server doesn't expose this endpoint, admins will manually enter all OAuth fields during enablement — they will not be blocked, but onboarding is slower and more error-prone

#### Choosing Your Auth Type

Four auth types are supported. Pick the one that matches **who owns the credential** for your server:

| Auth type | Who supplies the credential | Use when |
|-----------|----------------------------|----------|
| `userScopedToken` | The end-user, at request time via SDK metadata | Each user authenticates as themselves to the upstream service |
| `orgScopedToken` | Admin, during enablement | One shared org-level credential is used to call the upstream service for all users |
| `OAuth2_clientCredentials` | Server-to-server OAuth2 token | Machine-to-machine flows; no user context needed |
| `OAuth2_authorizationCode` | Each user, via interactive OAuth2 flow | Per-user delegated access with scopes the user consents to |



> **Header semantics**
>
> For `userScopedToken` and `orgScopedToken`, the outgoing header is always `{key}: Bearer {value}` (placeholders shown in braces). The `Bearer` scheme is hard-coded; `key` defaults to `Authorization` but admins may override it (for example, `X-API-Token`). Design your server to accept this format.



**A2A `securityScheme` → auth-type mapping:**

If you publish an A2A agent card, your declared `securitySchemes` are imported as follows:

| A2A scheme | Mapped auth types |
|------------|-------------------|
| `httpAuthSecurityScheme` (scheme: `Bearer`) | `userScopedToken`, `orgScopedToken` (admin chooses) |
| `apiKeySecurityScheme` (`in: header`) | `userScopedToken`, `orgScopedToken` (admin chooses) |
| `apiKeySecurityScheme` (`in: query` or `cookie`) | Rejected at registration |
| `oauth2.clientCredentials` | `OAuth2_clientCredentials` |
| `oauth2.authorizationCode` | `OAuth2_authorizationCode` |
| `openIdConnect`, `mtls` | Skipped (not supported) |

### Secrets Management

| Rule | Details |
|------|---------|
| Never log secrets | Redact tokens, keys, passwords from all log output |
| Never include in context | Secrets must not appear in tool outputs, error messages, or prompt content |
| Use short-lived tokens | Prefer STS-issued tokens with audience restrictions and proof-of-possession |
| Centralize storage | Integrate with vaults/KMS for at-rest encryption and leasing |
| Automate rotation | Rotate keys and certificates on schedule; support immediate revocation |
| No hardcoded secrets | Externalize all secrets from images, configs, and source code |

### Data Handling & Privacy

- **Minimize data collection** — only collect and send fields necessary for the operation
- **Classify data** — apply appropriate DLP rules for PII, secrets, and regulated data
- **Encrypt at rest** — use KMS envelope encryption with per-tenant keys
- **Encrypt in transit** — enforce TLS 1.2+ for all connections
- **Redact PII** from all logs, metrics, and telemetry
- **Define retention policies** — set TTLs, implement secure deletion, honor enterprise retention requirements
- **Isolate contexts** — prevent cross-session and cross-user data leakage
- **Limit context lifetime** — enforce quotas and TTLs for stored results and histories

### Supply Chain Security

- Use **trusted repositories** and signed packages for all dependencies
- Implement **version pinning** and lockfiles to prevent supply chain attacks
- Run **dependency scanning** (SCA) in CI/CD pipelines
- Produce **SBOMs** (Software Bill of Materials) and verify against known vulnerabilities
- Use **reproducible, signed builds** for deterministic artifact generation
- Require **digital signatures** for server packages and container images
- Audit new integrations and third-party libraries before adoption
- Restrict runtime permissions of hosted servers (network, disk, IPC)

### Network Security

- Enforce **HTTPS/TLS** for all server endpoints — no plaintext HTTP
- Restrict outbound connectivity with domain/IP **allowlists**
- Prevent **SSRF** — block requests to internal address spaces (RFC 1918, link-local, loopback)
- Apply **request normalization** — strip hop-by-hop headers, validate redirects
- Pin upstream certificates and validate DNS integrity
- For streaming (SSE/WebSocket): validate origins, enforce reconnection tokens, use heartbeats
- Enforce **maximum message sizes**, rate limits, and connection quotas

### Injection & Manipulation Defenses

**Prompt and tool injection:**
- Sanitize inputs before they reach LLMs or tool processing
- Use allowlisted command templates with typed parameters
- Scan tool descriptions for deceptive or conflicting metadata

**Tool name conflicts:**
- Implement unique namespace mapping (domain prefixes)
- Resolve priority based on verified metadata and admin policy
- Block shadowing patterns and downgrade attempts of legitimate tools

**Data-as-instructions ambiguity:**
- Maintain strict separation between data channels and instruction channels
- Strip or quarantine executable payloads found in data fields
- Validate content source and origin integrity for instruction-bearing content

---

## Reliability & Fault Tolerance

### Idempotency & Safe Retries

- **Design all state-changing operations to be idempotent**
- Support `Idempotency-Key` header or JSON-RPC request IDs
- Store pending requests and record completions to detect duplicates
- For truly non-idempotent actions (emails, purchases):
  - Return previous response without re-executing on retry
  - Add human confirmation steps before execution

**Implementation pattern:**
1. Receive request with idempotency key
2. Check if key exists in completion store
3. If exists → return stored response (no re-execution)
4. If not → execute, store result, return response

### Scaling & Failover

- Design for **stateless horizontal scaling** — any node should handle any request
- Store session/task checkpoints in external cache (Redis) or database
- Use session stickiness only for performance optimization, not correctness
- Buffer SSE events in external cache for reconnection support
- Implement health checks and graceful shutdown procedures

### Timeouts, Retries & Backoff

- Implement **timeouts** for all external calls, elicitations, and delegations
- Use **exponential backoff** with jitter for retries
- Return **structured errors** with machine-readable codes AND human-friendly messages
- Distinguish transient errors (retry-safe) from permanent errors (don't retry)

**Error response pattern:**
```json
{
  "error": {
    "code": "UPSTREAM_TIMEOUT",
    "message": "The calendar service did not respond within 30 seconds.",
    "retryable": true,
    "retryAfterSeconds": 5
  }
}
```

### Streaming & Reconnection

- Secure SSE/WebSocket with TLS; validate origins
- Attach **sequence numbers and timestamps** per message frame to prevent replay
- Support `Last-Event-ID` for resuming from last received event
- Enforce **idle timeouts** and heartbeat intervals
- Limit concurrent streams per client to prevent resource exhaustion
- Buffer events for a configurable duration (recommendation: 2–5 minutes)

---

## Observability & Governance

### Structured Logging

- Use structured JSON logs with **correlation IDs** across all requests
- Log every tool invocation with: tool name, sanitized arguments (no secrets), outcome, duration
- Propagate `X-Correlation-Id` headers through all downstream calls
- Redact secrets, tokens, and PII from all log output
- Include timestamps (ISO 8601/UTC), severity levels, and service identifiers

### Metrics & SLOs

Track and emit metrics for:

| Metric | Purpose |
|--------|---------|
| Requests per second (QPS) | Capacity planning |
| Latency (p50, p95, p99) | Performance SLOs |
| Error rate by code | Reliability tracking |
| Progress report frequency | UX quality |
| Queue depth | Backpressure detection |
| Token usage (LLM calls) | Cost visibility |

**Guidelines:**
- Tag metrics by tenant, tool name, and version
- Avoid high-cardinality tags (e.g., don't tag by user ID or request ID)
- Define internal SLOs for performance and cost; track against them
- Use OpenTelemetry for distributed tracing

### Audit Trails

- Maintain **tamper-evident audit logs** with integrity protection
- Log all privileged operations, policy decisions, and consent events
- Store audit entries with secure time sources (NTP-synced)
- Expose events for integration with SIEM and behavioral analytics systems
- Ensure audit logging happens **before** action execution (pre-action logging)

### Versioning & Deprecation

| Rule | Details |
|------|---------|
| Never break published schemas | Existing clients must continue to work |
| Additive changes only | Add optional fields → bump minor version |
| Breaking changes (rare) | Bump major version; keep old version live for several months |
| Deprecation window | Minimum several months with advance communication |
| Version fields | Include schema IDs and version fields in all JSON bodies |
| Deprecation warnings | Surface in annotation fields in response bodies |

---

## Testing & Evaluation

### Required Test Categories

| Category | What to Test |
|----------|-------------|
| **Contract tests** | Schema validation, required fields, error codes, idempotency behavior |
| **Integration tests** | End-to-end with real (or realistic mock) dependencies |
| **AI evaluations** | Typical prompts → verify correct tool selection and argument population |
| **Security tests** | Input injection, auth bypass, privilege escalation, SSRF |
| **Load/performance** | QPS, latency, memory under streaming, SSE reconnection |
| **Chaos tests** | Worker crash, connection drop, proxy timeout, partial failure |
| **Regression gates** | Re-run evaluations when underlying LLM models change |

### AI Evaluation Guidelines

- Create evaluation suites with representative prompts and expected tool selections
- Test that LLMs correctly populate required fields from conversation context
- Use tolerances and snapshots to distinguish acceptable variation from regression
- Re-evaluate periodically even without changes — model behavior can drift
- Test edge cases: ambiguous prompts, conflicting tools, missing required info

### Load & Cost Testing

- Benchmark with SSE enabled to capture streaming-specific performance
- Measure memory usage, QPS capacity, and perceived latency (time-to-first-byte)
- Track LLM token usage per operation — monitor for unexpected cost increases
- Validate graceful degradation under load (backpressure, admission control)

---

## Production Readiness Checklist

Before deploying to production, verify:

### Functionality
- [ ] All tool input/output schemas validated with contract tests
- [ ] Idempotency tested (happy path and failure/retry scenarios)
- [ ] Cancellation/abort handling tested
- [ ] Long-running operations stream progress and support resume
- [ ] Elicitation flows work correctly (happy path, timeout, denial)
- [ ] Error responses are structured with codes + friendly messages

### Security
- [ ] All inputs validated against JSON Schema; unknown fields rejected
- [ ] No string concatenation for SQL, shell, or template operations
- [ ] Authorization scopes declared per tool
- [ ] Secrets never logged, never in context, never in outputs
- [ ] PII redacted from all logs and telemetry
- [ ] Data encrypted at rest (KMS) and in transit (TLS)
- [ ] Supply chain: dependencies pinned, scanned, SBOM generated
- [ ] Network: outbound restricted, SSRF prevented, certificates pinned
- [ ] Security review completed and documented

### Reliability
- [ ] Streaming and reconnection tested (SSE drop/reconnect via Last-Event-ID)
- [ ] Timeouts configured for all external calls
- [ ] Exponential backoff with jitter for retries
- [ ] Graceful degradation under load verified
- [ ] Chaos tests passed (worker crash, proxy timeout, connection break)
- [ ] Health checks and graceful shutdown implemented

### Observability
- [ ] Structured logging with correlation IDs in place
- [ ] Metrics emitted: QPS, latency, error rates, queue depth
- [ ] SLOs defined and dashboards created
- [ ] Audit trails implemented for privileged operations
- [ ] Runbooks documented for common failure scenarios
- [ ] Alerting configured for SLO violations

### Governance
- [ ] Tool specifications match actual runtime behavior
- [ ] Friendly descriptions, tags, and documentation URLs provided
- [ ] Rate limits defined (per-user, per-client, per-tenant)
- [ ] Versioning strategy documented
- [ ] Deprecation policy in place for future changes

---

## Summary

Building a production-quality MCP or A2A server requires attention to:

1. **Design** — Right granularity, clear naming, precise schemas
2. **Security** — Defense-in-depth, input validation, least privilege, data minimization
3. **Reliability** — Idempotency, streaming resilience, graceful degradation
4. **Observability** — Structured logs, metrics, audit trails
5. **Testing** — Contract tests, AI evaluations, chaos testing, load benchmarks

Following these practices helps your server pass review efficiently, provide reliable service to AI agents, and meet enterprise security standards.
