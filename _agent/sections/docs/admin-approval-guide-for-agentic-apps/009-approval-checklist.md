---
type: Excerpt
canonical_url: https://developer.webex.com/docs/admin-approval-guide-for-agentic-apps
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Approval Checklist
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/admin-approval-guide-for-agentic-apps). [Full Markdown](../../../../docs/admin-approval-guide-for-agentic-apps.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Enablement Scope & Assignment](005-enablement-scope-assignment.md)

## Article introduction

---

This is a review guide for organization administrators evaluating and approving MCP Servers and A2A Agents before enabling them for organizational users. It provides guidelines to validate that an agentic app meets security, quality, and governance standards.

---

## Selected section

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
