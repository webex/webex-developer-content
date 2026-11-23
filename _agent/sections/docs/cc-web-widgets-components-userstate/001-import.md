---
type: Excerpt
canonical_url: https://developer.webex.com/docs/cc-web-widgets-components-userstate
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Import
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/cc-web-widgets-components-userstate). [Full Markdown](../../../../docs/cc-web-widgets-components-userstate.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The `UserState` component displays and manages the agent's current state in the contact center system.

---

The `UserState` component provides a user interface for agents to view and change their availability status. Common agent states include:

- `Available`
- `Meeting`
- Custom states (These can be set in the [Admin Portal](https://admin.webex.com))

Some of the states that can occur when call gets involved

**Non error cases**:

- `Engaged`
- `RONA` (Redirect On No Answer)

**Error cases**:

- `Invalid Number`
- `Unavailable`
- `Declined`
- `Busy`
- `Channel Failure`

**Look and feel**:
 1. ![1-userstate.png](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltebc8e6be1ceb2b23/6972a587c407ff2e807cb604/1-user-state.png?branch=integration&width=400)
 2. ![2-userstate.png](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt3308f10616dabd14/6972a587f63295607ec40e55/2-user-state.png?branch=integration&width=400)
 3. ![3-userstate.png](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt43216cb23c4a9e51/6972a58775543f601636390b/3-user-state.png?branch=integration&width=400)
 4. ![4-userstate.png](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt0b38b9f342767af4/6972a58733e29d70c839654b/4-user-state.png?branch=integration&width=400)
 5. ![5-userstate.png](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt8e4aacff68ecada5/6972a58790363d30b4c29726/5-user-state.png?branch=integration&width=400)

## Selected section

## Import

```js
import { UserState } from '@webex/cc-widgets';
```
