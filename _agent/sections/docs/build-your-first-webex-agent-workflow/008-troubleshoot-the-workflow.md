---
type: Excerpt
canonical_url: https://developer.webex.com/docs/build-your-first-webex-agent-workflow
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Troubleshoot the workflow
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/build-your-first-webex-agent-workflow). [Full Markdown](../../../../docs/build-your-first-webex-agent-workflow.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you start](002-before-you-start.md)

## Article introduction

Use VS Code with GitHub Copilot and the Webex Messaging MCP Server to inspect a test space, prepare an update, approve a single message, and verify the posted result.

## Selected section

## Troubleshoot the workflow

| What you observe | What to check |
| --- | --- |
| Server or tools are unavailable | Check the client connection, organization enablement, and allowed tools. Use the [connection troubleshooting guide](https://developer.webex.com/docs/webex-agentic-mcp-servers#troubleshooting). |
| A tool requests additional consent | Review the requested scope against the operation above. Grant only access appropriate to the test. |
| Access is denied | Check the account, space access, granted scopes, and administrator policy. Do not switch identities or destinations to bypass the denial. |
| Several spaces match | Resolve the intended room ID before drafting or posting. |
| The write has an uncertain result | Check for the unique marker before any new creation attempt. |
| Creation succeeds but read-back fails | Keep the returned identifier and inspect the space. Report verification as incomplete; do not create another message as a verification step. |
