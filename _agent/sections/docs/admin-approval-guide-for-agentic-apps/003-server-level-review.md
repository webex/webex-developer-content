---
type: Excerpt
canonical_url: https://developer.webex.com/docs/admin-approval-guide-for-agentic-apps
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Server-Level Review
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/admin-approval-guide-for-agentic-apps). [Full Markdown](../../../../docs/admin-approval-guide-for-agentic-apps.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Enablement Scope & Assignment](005-enablement-scope-assignment.md)

## Article introduction

---

This is a review guide for organization administrators evaluating and approving MCP Servers and A2A Agents before enabling them for organizational users. It provides guidelines to validate that an agentic app meets security, quality, and governance standards.

---

## Selected section

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
