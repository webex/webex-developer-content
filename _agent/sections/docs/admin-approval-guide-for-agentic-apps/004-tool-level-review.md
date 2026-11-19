---
type: Excerpt
canonical_url: https://developer.webex.com/docs/admin-approval-guide-for-agentic-apps
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Tool-Level Review
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/admin-approval-guide-for-agentic-apps). [Full Markdown](../../../../docs/admin-approval-guide-for-agentic-apps.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Enablement Scope & Assignment](005-enablement-scope-assignment.md)

## Article introduction

---

This is a review guide for organization administrators evaluating and approving MCP Servers and A2A Agents before enabling them for organizational users. It provides guidelines to validate that an agentic app meets security, quality, and governance standards.

---

## Selected section

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
