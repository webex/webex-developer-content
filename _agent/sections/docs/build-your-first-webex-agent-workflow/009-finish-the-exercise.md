---
type: Excerpt
canonical_url: https://developer.webex.com/docs/build-your-first-webex-agent-workflow
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Finish the exercise
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/build-your-first-webex-agent-workflow). [Full Markdown](../../../../docs/build-your-first-webex-agent-workflow.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you start](002-before-you-start.md)

## Article introduction

Use VS Code with GitHub Copilot and the Webex Messaging MCP Server to inspect a test space, prepare an update, approve a single message, and verify the posted result.

## Selected section

## Finish the exercise

Disable the message-creation tool when you no longer need it. If you want to remove the test message, inspect the exact message in the Webex app and delete it manually; do not ask the agent to delete a space or unrelated content. If the connection was temporary, remove it using your client's supported controls and follow the [WCIT revocation guidance](https://developer.webex.com/docs/webex-agentic-mcp-servers#revoking-your-wcit-token) when the token is no longer needed.

Keep a record of the destination check, cancelled attempt, approved creation, and independent read-back. These checks give you a repeatable starting point for a more useful workflow. Continue with the [Agent Skills overview](https://developer.webex.com/docs/agent-skills-overview) to learn how reusable instructions can guide recurring tasks.
