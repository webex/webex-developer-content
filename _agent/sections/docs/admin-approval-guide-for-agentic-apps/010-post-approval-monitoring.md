---
type: Excerpt
canonical_url: https://developer.webex.com/docs/admin-approval-guide-for-agentic-apps
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Post-Approval Monitoring
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/admin-approval-guide-for-agentic-apps). [Full Markdown](../../../../docs/admin-approval-guide-for-agentic-apps.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Enablement Scope & Assignment](005-enablement-scope-assignment.md)

## Article introduction

---

This is a review guide for organization administrators evaluating and approving MCP Servers and A2A Agents before enabling them for organizational users. It provides guidelines to validate that an agentic app meets security, quality, and governance standards.

---

## Selected section

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
