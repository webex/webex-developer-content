---
type: Excerpt
canonical_url: https://developer.webex.com/docs/become-a-byova-provider
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Provider and customer responsibilities
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/become-a-byova-provider). [Full Markdown](../../../../docs/become-a-byova-provider.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md)

## Article introduction

Build and operate a Webex App Hub Service App that securely connects your virtual agent gateway to each customer's Webex Contact Center organization.

## Selected section

## Provider and customer responsibilities

| Provider | Customer |
| --- | --- |
| Publishes and operates the App Hub Service App and its token-management path | Reviews scopes and authorizes the Service App |
| Operates the secure BYOVA gateway | Confirms BYOVA is available in the Contact Center organization |
| Creates, renews, and monitors the organization datasource | Creates the Virtual Agent feature |
| Provides the datasource ID and flow template | Binds the feature to a Flow Designer flow |
| Disables access after deauthorization | Publishes, routes, and tests call behavior |
