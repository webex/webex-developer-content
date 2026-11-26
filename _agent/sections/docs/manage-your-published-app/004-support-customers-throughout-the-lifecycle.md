---
type: Excerpt
canonical_url: https://developer.webex.com/docs/manage-your-published-app
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Support customers throughout the lifecycle
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/manage-your-published-app). [Full Markdown](../../../../docs/manage-your-published-app.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Plan application and permission changes](003-plan-application-and-permission-changes.md)

## Article introduction

Keep your App Hub listing accurate, support customers through changes, and plan updates or retirement alongside the authorization lifecycle of your app.

## Selected section

## Support customers throughout the lifecycle

Provide customers with a support path for your application and distinguish application issues from Webex platform issues. For a platform investigation, include the affected workflow, time and timezone, error details, and available request or tracking identifiers. Share only the information needed to investigate; remove credentials and unnecessary personal data.

Test recovery for expired credentials, declined authorization, interrupted setup, and unavailable dependencies. Use the [Authentication](https://developer.webex.com/docs/authentication) and [Service Apps](https://developer.webex.com/docs/service-apps) guides for the relevant credential flow, and [Webhooks](https://developer.webex.com/docs/webhooks) for event-driven workflows.

For BYOVA, follow [Maintain the DataSource Connection](https://developer.webex.com/docs/become-a-byova-provider#maintain-the-datasource-connection) and [Handle Deauthorization and Offboarding](https://developer.webex.com/docs/become-a-byova-provider#handle-deauthorization-and-offboarding). Keep each customer's authorization and provisioning state separate.

Monitor the [API Changelog](https://developer.webex.com/docs/api/changelog) and [API and SDK Support Policy](https://developer.webex.com/docs/webex-api-and-sdk-support-policy) for changes that affect your dependencies. Test relevant updates before customers reach a migration deadline.
