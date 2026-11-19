---
type: Guide
title: Security Guides | Admin Approval Guide
display_title: Admin Approval Guide for Agentic Apps
canonical_url: https://developer.webex.com/docs/admin-approval-guide-for-agentic-apps
content_type: documentation
product_group:
- webex-suite
- webex-contact-center
categories:
- app-hub
- mcp
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/admin-approval-guide-for-agentic-apps)

---

This is a review guide for organization administrators evaluating and approving MCP Servers and A2A Agents before enabling them for organizational users. It provides guidelines to validate that an agentic app meets security, quality, and governance standards.

---

## Table of Contents

- [Overview](#overview)
- [Server-Level Review](#server-level-review)
  - [Identity & Provenance](#identity--provenance)
  - [Server Accessibility](#server-accessibility)
  - [Authentication Configuration](#authentication-configuration)
  - [Privacy & Compliance](#privacy--compliance)
  - [Badge Types (Public Apps on AppHub)](#badge-types-public-apps-on-apphub)
- [Tool-Level Review](#tool-level-review)
  - [Tool Naming & Descriptions](#tool-naming--descriptions)
  - [Input & Output Schemas](#input--output-schemas)
  - [Side Effects & Risk Assessment](#side-effects--risk-assessment)
  - [Consent & Elicitation Requirements](#consent--elicitation-requirements)
- [Enablement Scope & Assignment](#enablement-scope--assignment)
  - [Org vs. Group Enablement](#org-vs-group-enablement)
  - [Shared vs. Per-Function Assignment](#shared-vs-per-function-assignment)
- [Security Review](#security-review)
  - [Input Validation Posture](#input-validation-posture)
  - [Authorization & Least Privilege](#authorization--least-privilege)
  - [Data Handling & Privacy](#data-handling--privacy)
  - [Network & Supply Chain](#network--supply-chain)
  - [Injection & Manipulation Defenses](#injection--manipulation-defenses)
- [Quality Review](#quality-review)
  - [Functional Accuracy](#functional-accuracy)
  - [Error Handling](#error-handling)
  - [Reliability & Performance](#reliability--performance)
  - [Documentation & Support](#documentation--support)
- [Signature & Change Policy](#signature--change-policy)
- [Approval Checklist](#approval-checklist)
- [Post-Approval Monitoring](#post-approval-monitoring)

---

## Overview

### Your Role as Gatekeeper

As an organization administrator, you are responsible for ensuring that any agentic app enabled for your users meets your organization's security, privacy, and quality standards. Agentic apps have the ability to:

- Execute actions on behalf of users via AI agents
- Access organizational data through configured credentials
- Interact with external systems using your org's identity

**Before approving an app, verify that:**
1. The developer/company is legitimate and trustworthy
2. The server and its tools are secure and well-designed
3. The data handling practices align with your org's policies
4. The capabilities exposed are appropriate for your user base

### Review Process

1. **Browse** → Discover the app in Control Hub → Management → Apps → Agentic Servers
2. **Review** → Evaluate the app
3. **Configure** → Set authentication, enable specific tools, define scope
4. **Approve** → Enable for your organization (org-wide or group-specific)
5. **Monitor** → Observe usage and re-review on changes

---

## Server-Level Review

### Identity & Provenance

Verify the app's publisher is legitimate and the server is production-ready.

| Check | What to Verify | Red Flags |
|-------|---------------|-----------|
| Company name | Real company; matches contact email domain | Unknown company, mismatched domains |
| Developer identity | For org-private apps: verify developer within your org. For public apps: rely on Cisco's review (developer account details are not visible to org admins) | For org-private: unknown developer within org |
| Company website | Valid, accessible, professional | Placeholder sites, parked domains |
| App description | Clear, specific, matches actual functionality | Vague descriptions, marketing-only language, mentions "demo" or "alpha" |
| Logo & branding | Professional; no Cisco/Webex branding (unless Cisco app) | Low quality, appropriated branding |
| Badge type | Check the badge assigned on AppHub (see badge types below) | No badge, or Federated badge without additional due diligence |

#### Badge Types (Public Apps on AppHub)

Public agentic apps are assigned a badge on AppHub indicating the level of Cisco review they have undergone:

| Badge | Meaning | Trust Level |
|-------|---------|-------------|
| **Cisco Official** | Cisco Official; Certified by Cisco (first-party or OEM) | Highest — developed/maintained by Cisco |
| **Cisco Onboarded** | Developed by external party; Certified by Cisco | High — passed Cisco certification |
| **Partner Onboarded** | Developed by Cisco Partner; Reviewed by Cisco | High — partner-vetted and Cisco-reviewed |
| **Developer Onboarded** | Developed by independent developer; Reviewed by Cisco | Moderate — passed Cisco's review process |
| **Federated through Registry** | Imported from External Registry; no Cisco manual review | Lower — has NOT undergone Cisco's manual review; exercise extra due diligence |



> **Org-Private vs. Public**
>
> **Org-Private apps** are only visible to your organization. They have NOT undergone any Cisco/AppHub review. As the org admin, you are solely responsible for reviewing and approving these apps. **Public apps** have been reviewed by Cisco and carry a badge indicating the level of review (see table above). However, even for public apps, the org admin remains ultimately responsible for enabling the app within their organization. Cisco's review validates technical and security standards, but the decision to allow the app for your users — and the associated legal and compliance responsibility — rests with you as the org administrator.

 

### Server Accessibility

| Check | What to Verify |
|-------|---------------|
| Server URL | Valid HTTPS endpoint, publicly reachable |
| TLS certificate | Valid, not expired, issued by trusted CA |
| Response time | Server responds within acceptable latency |
| Availability | Server has documented uptime SLAs or reliability history |

### Authentication Configuration

Ensure the authentication type is appropriate for the server's purpose and your org's security posture. Agent Central supports four auth types:

| **Auth Type** | **When Appropriate** | **What You Configure** | **Admin Concern** |
|-----------|-----------------|--------------------|---------------|
| **OAuth 2.0 – Client Credentials** (`OAuth2_clientCredentials`) | Server-to-server; no user context needed | `clientId`, `clientSecret`, `authServerURL`, `scope` | Verify token endpoint is legitimate; check scope breadth |
| **OAuth 2.0 – Authorization Code** (`OAuth2_authorizationCode`) | User-delegated access; interactive flows | `clientId`, `clientSecret`, `authServerURL`, `authorizationEndpoint`, `scope`, `registrationEndpoint`, `tokenEndpointAuthMethod` | Verify authorization endpoint; assess PKCE support; check scope granularity |
| **Org-Scoped Token** (`orgScopedToken`) | Admin-provisioned shared credential (e.g., API key); same token used for all users | `key` (header name, default `Authorization`) + `value` (KMS-encrypted at rest) | Verify the credential is scoped narrowly; confirm rotation plan; understand who else has access |
| **User-Scoped Token** (`userScopedToken`) | End-user supplies token at runtime via SDK; each user authenticates as themselves | Only `key` (header name, default `Authorization`) — no value persisted | Users are directly authenticating; understand what access the token grants to the server |



> **Header semantics**
>
> For `userScopedToken` and `orgScopedToken`, the credential is sent as `{key}: Bearer {value}` (placeholders shown in braces). The `Bearer` scheme is hard-coded; the `key` field controls only the header name. If the upstream server expects a non-`Authorization` header (e.g., `X-API-Token`), set `key` accordingly during enablement.





> **Credential storage**
>
> `orgScopedToken.value`, `OAuth2.clientSecret`, and OAuth2 access tokens are KMS-encrypted at rest. `userScopedToken` never persists a token value — it's supplied per-request by the client SDK.





> **Legacy auth types**
>
> Legacy auth types `apiKey` and `userToken` are automatically migrated on read to `orgScopedToken` and `userScopedToken` respectively. `customHeaderAuth` is **rejected for new server registrations** but still honored on read for existing records (admin enablement writes still accept it for back-compat).





> **OAuth configuration prefill**
>
> For OAuth auth types, if the server exposes a `.well-known/oauth-authorization-server` endpoint (RFC 8414), the authorization endpoint, token endpoint, and supported scopes are automatically prefilled during enablement. If the server does not expose this endpoint, you (the admin) will need to manually fill in these OAuth configuration values.



**Questions to ask:**
- Does the auth type match the data sensitivity level? (Shared org credential vs. per-user identity matter very differently for audit and blast radius.)
- Are credentials rotatable? What is the rotation schedule?
- Are scopes minimal (least privilege)?
- For OAuth: Is the authorization server well-known and trusted? Are the prefilled values correct?
- For `orgScopedToken`: Is the stored credential KMS-encrypted and rotated regularly? Who in your org has visibility into the value?
- For `userScopedToken`: Is the header `key` appropriate for the upstream service, or is the default `Authorization` header sufficient?

### Privacy & Compliance

Vendor-provided URLs are captured and displayed as part of server metadata. Review the following:

| Check | What to Verify |
|-------|---------------|
| Privacy URL (`privacyUrl`) | Valid, publicly accessible link that explains data handling |
| Support URL (`supportUrl`) | Valid link for issue reporting and support |
| Company URL (`companyUrl`) | Matches the publisher's claimed identity |
| Product URL (`productUrl`) | Points to legitimate product documentation |

---

## Tool-Level Review

Review **each tool individually** before enabling it. Tools are the primary attack surface for agentic apps.

### Tool Naming & Descriptions

| Check | What to Look For | Red Flags |
|-------|-----------------|-----------|
| Name clarity | Descriptive, uses domain prefix + verb pattern | Generic names (`run`, `execute`); no domain prefix |
| Name length | ≤ 60 characters | Excessively long or abbreviated names |
| Description accuracy | Matches actual behavior; factual and neutral | Imperative language ("always use this tool"); exaggerated claims |
| No manipulation | Description doesn't try to influence LLM preference | Phrases like "preferred tool", "use this instead of..." |
| Namespace uniqueness | Doesn't shadow or conflict with other server tools | Identical names to common tools from other servers |



> **Why this matters**
>
> Tool descriptions are injected into LLM context. Deceptive descriptions can manipulate which tools get selected, potentially routing sensitive data to malicious servers.



### Input & Output Schemas

| Check | What to Verify | Red Flags |
|-------|---------------|-----------|
| Schema precision | Uses explicit types, constraints, enums, bounds | Unbounded strings, `any` types, no validation |
| Required fields | Clearly marked; minimal set | Everything optional (tool may silently fill defaults) |
| No excessive data collection | Input fields are necessary for the stated function | Requesting user data unrelated to tool purpose |
| Output structure | Outputs are concise and well-typed | Large unstructured text dumps; excessive data return |
| Sensitive field handling | PII/secrets marked; guardrails declared | No sensitivity annotations; potential data leakage paths |
| Additional properties | `additionalProperties: false` prevents unexpected input | Schema allows arbitrary extra fields |

### Side Effects & Risk Assessment

Tools don't carry a formal risk-class field — **you assess risk from the tool's name, description, input schema, and stated side effects.** Use the buckets below as a mental model when deciding whether to enable a tool, restrict it to specific groups, or reject it.

| Your Assessment | Examples | Review Scrutiny |
|-----------------|---------|-----------------|
| **High** | Delete operations, financial transactions, sending emails, modifying user data | Requires strongest justification; consider restricting to specific groups (`enablementLevel: group` with `assignmentMode: perTool`) |
| **Medium** | Read with broad scope, modify non-critical settings, create non-sensitive records | Standard review; verify scope is appropriate |
| **Low** | Read-only lookups, status checks, formatting operations | Light review; verify data returned is appropriate |

**Questions for tools you assess as high-risk:**
- Does the tool description indicate a human-in-the-loop step (elicitation) before execution?
- Can the action be undone if invoked incorrectly?
- Is the scope of impact bounded (single user vs. org-wide)?
- Does the tool advertise rate limits preventing mass actions?

### Consent & Elicitation Requirements

Elicitation is the developer-facing mechanism for pausing a tool call to ask the user for input or confirmation. As an admin, you can't directly configure elicitation — but you can assess whether the developer has applied it appropriately.

| Check | What to Verify |
|-------|---------------|
| Description signals consent steps | Description indicates when user input or confirmation is required mid-execution |
| Destructive operations are gated | Tools you assessed as high-risk pause for explicit user confirmation rather than acting silently |
| Headless behavior is documented | The developer documents what happens when no user is present (e.g., automated pipelines) |
| Elicitation prompts are clear | If the tool elicits input, the prompts shown to the user are factual and non-misleading |

---

## Enablement Scope & Assignment

When you approve an MCP server, you also decide **who in your org may use it** and **at what granularity**. The **General** tab in Control Hub uses the following labels:

| Dimension | Choices |
|-----------|---------|
| Audience | **Allowed for all users** or **Limited access** |
| Assignment mode under **Limited access** | **Same groups for all functions** or **Different groups per function** |

Use **Blocked for all users** when the server should not be available to your organization. Follow [Provisioning on Control Hub](https://developer.webex.com/docs/provisioning-on-control-hub#group-level-access) for configuration steps. Group-level access does not apply to MCP actions in Webex AI Agent Studio; those actions use organization-level access.

### Org vs. Group Enablement

| Choice | When to Use | Trade-off |
|--------|------------|-----------|
| **Allowed for all users** | Low-risk, broadly useful tools (e.g., calendar lookups, generic search) | Makes enabled functions discoverable to all users in your organization |
| **Limited access** | Functions intended for selected groups, such as role-specific workflows | Limits enabled-function discovery by group membership; requires current group lists |

With **Limited access**, you choose the groups that should discover the server's enabled functions. Discovery compares the user's groups from your organization's identity with the configured groups. A function appears only when at least one group matches. These settings govern enabled-function discovery; the MCP server's own authentication and authorization controls still apply when a function is invoked.

### Shared vs. Per-Function Assignment

| Choice | Behavior | When to Use |
|--------|---------|------------|
| **Same groups for all functions** | The selected groups apply to all enabled tools, resources, and prompts | Most apps. Simpler to reason about; fewer settings to maintain |
| **Different groups per function** | Each function has its own group selection, configured on **Tools**, **Resources**, or **Prompts** | Apps where some functions need a different audience from others |



> **Best Practice**
>
> Start with **Same groups for all functions**. Choose **Different groups per function** when functions need different audiences. Review each function's group list regularly to keep access aligned with your intent.



---

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

## Quality Review

### Functional Accuracy

| Check | What to Verify |
|-------|---------------|
| Description matches behavior | Tool does what its description says — no more, no less |
| No hidden functionality | Tool doesn't perform undisclosed actions |
| Predictable behavior | Same inputs produce consistent, expected outputs |
| Error states documented | Known failure modes are described |
| Edge cases handled | Tool behaves gracefully with boundary inputs |

### Error Handling

| Check | What to Verify |
|-------|---------------|
| Structured errors | Errors return machine-readable codes + human-friendly messages |
| No information leakage | Error messages don't expose internal details, stack traces, or secrets |
| Graceful degradation | Tool doesn't crash or hang on invalid input |
| Retry guidance | Errors indicate whether retry is safe (`retryable` flag) |

### Reliability & Performance

| Check | What to Verify |
|-------|---------------|
| Response time | Tools respond within reasonable timeouts |
| Progress streaming | Long operations provide progress feedback |
| Reconnection support | SSE/streaming supports `Last-Event-ID` resume |
| Rate limiting | Server enforces fair-use limits |
| Idempotency | State-changing operations handle retries safely |

### Documentation & Support

| Check | What to Verify |
|-------|---------------|
| Documentation URL | Valid, accessible developer documentation |
| Support channel | Clear path for reporting issues |
| Changelog/versioning | Version history available; deprecation policy stated |
| SLA/uptime | Service level expectations documented |

---

## Signature & Change Policy

### Understanding Tool Signatures

Webex computes a schema signature for each tool and continuously monitors it for changes. When a tool's current signature differs from the version you previously approved, Webex flags it: the tool's behavior may have been modified since your last review.

### When Signatures Change

| Scenario | What Changed | Risk Level | Recommended Action |
|----------|-------------|-----------|-------------------|
| Description update (cosmetic) | Wording improved, no semantic change | Low | Review, re-approve |
| New optional input field | Schema expanded (non-breaking) | Medium | Verify field purpose; re-approve |
| Required field added/removed | Schema breaking change | High | Full re-review required |
| Input validation changed | Constraints tightened or loosened | Medium-High | Assess security impact |
| Tool renamed | Name changed (signature changes) | High | Effectively a new tool; full review |

### Configuring Signature Policy

For each tool, decide on **"Allow signature change"**:

| Setting | When to Use | Trade-off |
|---------|------------|-----------|
| **Off** (recommended for high-security) | Sensitive operations; regulated environments | Users lose access until you re-review; more admin work |
| **On** (acceptable for low-risk) | Read-only tools; trusted publisher with good track record | Reduced admin burden; accepts risk of unreviewed changes |



> **Best Practice**
>
> Default to **Off** for new/unfamiliar servers. Switch to **On** only after establishing trust with the publisher through multiple successful review cycles.



### Runtime Behavior on Signature Drift

When a tool's live signature differs from the stored signature:

| `Allow signature change` | Tool delivered to client SDK? | `unsecure` flag set? |
|--------------------------|------------------------------|----------------------|
| **Off** | No — tool is filtered out of `/listFunctions` results | n/a |
| **On** | Yes — tool is still delivered | **Yes** — `unsecure: true` is included on the tool, so client SDKs and agent UIs can surface a warning to end users |

The `unsecure` flag is your safety net when running with `Allow signature change = On`: clients still receive the tool, but they're alerted that the contract has shifted since you last reviewed it.

---

## Approval Checklist

Use this checklist before enabling an agentic app.

### Server Identity & Trust

- [ ] Publisher is a legitimate, identifiable company
- [ ] Company website is valid and professional
- [ ] Contact email domain matches company name
- [ ] App description clearly states purpose and capabilities
- [ ] Logo is appropriate and original (no Cisco/Webex branding misuse)
- [ ] Badge type reviewed and understood (for public apps)
- [ ] Privacy URL (`privacyUrl`) is publicly accessible
- [ ] Support URL (`supportUrl`) is valid and accessible
- [ ] For org-private apps: developer identity verified within your org

### Security

- [ ] Server URL uses HTTPS with valid TLS certificate
- [ ] Authentication type is appropriate for data sensitivity
- [ ] OAuth scopes (if applicable) are minimal and well-defined
- [ ] No tool requests excessive or unnecessary permissions
- [ ] Input schemas enforce strict validation (types, bounds, patterns)
- [ ] No evidence of dynamic code execution from user input
- [ ] Tool descriptions are factual and don't contain manipulative/injection content

### Tool Quality

- [ ] Tool names are clear, descriptive, and properly namespaced
- [ ] Tool descriptions are accurate, factual, and non-manipulative
- [ ] Input/output schemas are precise with appropriate constraints
- [ ] High-risk tools have human-in-the-loop (elicitation) controls
- [ ] Error handling produces structured, non-leaking responses
- [ ] Side effects are documented and appropriate for stated purpose
- [ ] No tool appears to shadow or impersonate tools from other servers

### Privacy & Data Handling

- [ ] Privacy URL points to a valid, accessible policy page
- [ ] Data minimization: tools only request/return data necessary for their function
- [ ] No tool collects input fields unrelated to its stated purpose
- [ ] Cross-session data isolation: no data leakage between users or sessions
- [ ] User consent mechanisms are in place for sensitive/destructive operations

### Enablement Scope

- [ ] Audience choice (**Allowed for all users** vs. **Limited access**) matches the server's risk profile
- [ ] If **Limited access**: group lists are current and reflect the intended audience
- [ ] Group assignment mode (**Same groups for all functions** vs. **Different groups per function**) matches whether functions need different audiences
- [ ] **Allow signature change** set per tool — default to **Off** for new/unfamiliar servers

### Operational Readiness

- [ ] Documentation/support URL is valid and useful
- [ ] Version and changelog information available
- [ ] Rate limiting is in place
- [ ] Long-running operations support progress streaming
- [ ] Server demonstrates acceptable response times
- [ ] Reconnection/resume supported for streaming operations

---

## Post-Approval Monitoring

After enabling an agentic app, continue to monitor for issues.

Webex automatically detects changes in server metadata, enablement state, and tool schema signatures, and surfaces them in your admin views. You don't need to poll — the system tells you what changed.

### What to Watch For

| Signal | Detected by | Action |
|--------|------------|--------|
| Tool signature change | Schema signature comparison | Review notification; re-evaluate if `Allow signature change` is **Off** (tool will be filtered out until re-approved). If **On**, the tool is delivered with `unsecure: true` until you re-approve. |
| Server metadata change | Developer edits to description, serverUrl, authType, publish data, submission status | Confirm the change is benign (cosmetic vs. functional). Re-review on URL or authType changes. |
| Enablement change | Admin writes to enablement, auth config, or custom headers | Audit trail — confirm change was authorized |
| Unusual usage patterns | Operational telemetry | Investigate spikes in invocations or error rates |
| User complaints | Out-of-band | Investigate tool behavior discrepancies |
| Security advisories | Out-of-band (vendor / CVE feeds) | Check if server's dependencies have known vulnerabilities |
| Version bumps | Server metadata change | Review changelog for breaking changes or new capabilities |
| Server downtime | Health checks | Monitor availability; consider disabling if prolonged |

### When to Re-Review

Trigger a full re-review when:
- Tool signatures change (if policy is "Off")
- Major version bump announced by the developer
- Security incident reported affecting the server or its dependencies
- Org security policy changes (e.g., stricter data residency requirements)
- User reports unexpected behavior or data exposure
- More than 6 months since last review (periodic hygiene)

### Revoking Approval

If a server no longer meets standards:
1. Toggle the app to **Blocked** in Control Hub (immediate effect)
2. Document the reason for revocation
3. Notify affected users/groups
4. Contact the developer with specific issues for remediation
5. Re-review if/when the developer addresses concerns

---

## Summary

Effective approval requires evaluating an agentic app across four dimensions:

| Dimension | Key Questions |
|-----------|--------------|
| **Trust** | Is the publisher legitimate? Is this a production-quality app? |
| **Security** | Are inputs validated? Are privileges minimal? Is data protected? |
| **Quality** | Do tools work as described? Are errors handled gracefully? |
| **Governance** | Can you maintain oversight? Are changes tracked and reviewable? |

When in doubt, start with a **restrictive posture**: enable only specific tools, limit to a pilot group, keep signature change policy off, and expand access as trust is established through operational experience.
