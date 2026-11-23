---
type: Excerpt
canonical_url: https://developer.webex.com/docs/api-and-sdk-support-policy
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- APIs and SDKs end of life (EOL) policy
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/api-and-sdk-support-policy). [Full Markdown](../../../../docs/api-and-sdk-support-policy.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Selected section

## APIs and SDKs end of life (EOL) policy 

### Normal Upgrade Cycle

**API** versions will be deprecated 18 months after the release of a new version.

- At the time of the new release, a notification will be sent to all customers that a new version is available including the change log of what was added or fixed.
- After 12 months customers still using deprecated APIs will be contacted with an ever increasing frequency being asked to upgrade.
- At the 18 months mark the deprecated APIs shall be switched off using 410 HTTP code.

**SDK** versions will be deprecated 12 months after the release of a new minor version or 18 months in case of a major version.

- At the time of the new release, Cisco will communicate to the community about the changes that are included in the new version and reminders to upgrade.
- At 18 months mark the deprecated SDK may stop functioning. Attempts shall be made on Cisco's part to help customer apps "fail gracefully" in such cases.

### Priority Upgrade Policy

A **priority** upgrade will be required if there is an issue discovered that impacts Webex' ability to maintain quality of service. If a priority upgrade is required for the API or an SDK, the old versions will be supported up to 6 months from the time of release of the new version.

### Critical Upgrade Policy

A **critical** upgrade will be limited to changes that are required to remediate security and/or data protection or loss issues. If a critical upgrade is required for the API or an SDK, the old versions will be immediately deprecated at the time of release of the new version.

- Connections from previous version may be refused immediately.
- At the time of the new release, a notification will be sent to all customers using the existing version that a new version is available to address a critical issue and include appropriate details of the impact of the critical issue. Instructions will be provided on how to upgrade to the new version as soon as possible with an offer of assistance from support.
- Technical support and Customer Success will work with all affected teams until upgrades are completed.
