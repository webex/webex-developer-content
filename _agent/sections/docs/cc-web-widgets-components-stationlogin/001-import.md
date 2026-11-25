---
type: Excerpt
canonical_url: https://developer.webex.com/docs/cc-web-widgets-components-stationlogin
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Import
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/cc-web-widgets-components-stationlogin). [Full Markdown](../../../../docs/cc-web-widgets-components-stationlogin.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The `StationLogin` component allows agents to perform station login and select the type of channel they want to use for establishing voice connections.

---

The `StationLogin` component provides a user interface for agents to log in to their contact center station and choose from different connection types:

- **Desktop**: Uses WebRTC for voice communication
- **Extension**: Allows using a softphone or a hardphone extension
- **Dial Number**: Allows using a PSTN phone number

**Look and feel**:

When profile mode is not enabled

 1. ![1-station-login.png](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt1d5c701c7da5b6e1/6972a49190363d5380c29719/1-station-login.png?branch=integration&width=560)
 2. ![2-station-login.png](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt1450dc2fb97d08f5/6972a49133e29d9740396545/2-station-login.png?branch=integration&width=560)
 3. ![3-station-login.png](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte0a2c877cfa2cff9/6972a491821629a776931257/3-station-login.png?branch=integration&width=560)
 4. ![4-station-login.png](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt739a744b7aacbe4d/6972a49190363d3327c29715/4-station-login.png?branch=integration&width=560)

When profile mode is enabled

![5-station-login.png](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt6317c86469143512/6972a491f19f60601b999ec6/5-station-login-profile-mode.png?branch=integration&width=560)

**Note**: When profile mode is enabled, you can change your StationLogin mode.

## Selected section

## Import

```js
import { StationLogin } from '@webex/cc-widgets';
```
