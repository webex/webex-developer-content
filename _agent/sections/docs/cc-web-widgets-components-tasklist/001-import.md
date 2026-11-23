---
type: Excerpt
canonical_url: https://developer.webex.com/docs/cc-web-widgets-components-tasklist
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Import
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

## Import

```js
import { TaskList } from '@webex/cc-widgets';
```
