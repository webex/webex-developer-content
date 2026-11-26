---
type: Excerpt
canonical_url: https://developer.webex.com/docs/cc-web-widgets-components-outdialcall
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Configuration Notes
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/cc-web-widgets-components-outdialcall). [Full Markdown](../../../../docs/cc-web-widgets-components-outdialcall.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The `OutdialCall` component enables agents to make outbound calls directly from the contact center interface.

---

The `OutdialCall` component provides a user interface for agents to initiate outbound calls to customers or other parties. This component is essential for:

- Proactive customer outreach
- Return calls to customers
- Callback campaigns
- Outbound sales or service calls

**Look and feel**:
1. ![1-outdial-call.png](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt7fd1f8ae03bacd40/6972a414f19f6074f5999ec2/1-outdial-call.png?branch=integration&height=400)
2. ![2-outdial-call.png](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blteea85e80d89ccbdf/6972a41475543f273c3638fd/2-outdial-call.png?branch=integration&height=400)
3. ![3-outdial-call.png](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt4e9f7256328765a0/6972a4140398574b2c825e02/3-outdial-call.png?branch=integration&height=400)

## Selected section

## Configuration Notes

- Outbound calls can only be initiated when the agent does not have any other active voice calls
- Outdial permissions must be configured in the contact center system through the [Admin Portal](https://admin.webex.com).
- The `store` must be initialized with a valid access token
- Make sure to wrap the component with `ThemeProvider` and `IconProvider` from Momentum Design
- Address Book contacts must be configured in the contact center system through the [Admin Portal](https://admin.webex.com) for the feature to display available contacts
