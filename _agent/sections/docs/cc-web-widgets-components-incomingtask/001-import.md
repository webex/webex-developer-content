---
type: Excerpt
canonical_url: https://developer.webex.com/docs/cc-web-widgets-components-incomingtask
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Import
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/cc-web-widgets-components-incomingtask). [Full Markdown](../../../../docs/cc-web-widgets-components-incomingtask.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The `IncomingTask` component presents incoming tasks to agents and provides actions to accept or reject them.

---

The `IncomingTask` component displays incoming contact center tasks (such as calls, chats, emails) and allows agents to take action on them. The component provides a clear interface for agents to:

- View incoming task details
- Accept incoming tasks (For **Desktop** calls only)
- Decline incoming tasks (For **Desktop** calls only)

**Look and feel**:

![incoming-task.png](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt92631c28fffeeb81/6972a15f446329996b6a3f21/incoming-task.png?branch=integration&width=560)

## Selected section

## Import

```js
import { IncomingTask } from '@webex/cc-widgets';
```
