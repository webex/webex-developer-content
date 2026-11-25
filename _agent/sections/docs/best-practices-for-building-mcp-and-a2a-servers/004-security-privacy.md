---
type: Excerpt
canonical_url: https://developer.webex.com/docs/best-practices-for-building-mcp-and-a2a-servers
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Security & Privacy
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/best-practices-for-building-mcp-and-a2a-servers). [Full Markdown](../../../../docs/best-practices-for-building-mcp-and-a2a-servers.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

---

This is a guide for developers building MCP Servers and A2A Agents for the Webex ecosystem. Following these practices helps your server be secure, reliable, and performant while delivering a consistent experience for AI agents and end users.

---

## Selected section

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
