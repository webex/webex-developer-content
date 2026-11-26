---
type: Excerpt
canonical_url: https://developer.webex.com/docs/cc-web-widgets-components-tasklist
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Configuration Notes
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/cc-web-widgets-components-tasklist). [Full Markdown](../../../../docs/cc-web-widgets-components-tasklist.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The `TaskList` component renders and manages a list of active tasks for the agent.

---

It provides a comprehensive view of all active tasks assigned to the agent. It allows agents to:

- View multiple tasks simultaneously
- Select tasks to focus on
- Accept/Decline pending tasks from the list
- See task details and status

**Look and feel**:

![task-list](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt58315177e3fbe15c/6972a51190363d3dbac2971e/task-list.png?branch=integration&width=560)

## Selected section

## Configuration Notes

- The component requires the `store` to be initialized with a valid access token
- Agents must be logged in and in an appropriate state to see tasks
- Make sure to wrap the component with `ThemeProvider` and `IconProvider` from Momentum Design
