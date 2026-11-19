---
type: Excerpt
canonical_url: https://developer.webex.com/docs/app-hub-build-and-test
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Map the workflow to app components
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/app-hub-build-and-test). [Full Markdown](../../../../docs/app-hub-build-and-test.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Continue to submission and customer setup](006-continue-to-submission-and-customer-setup.md)

## Article introduction

Turn your chosen app type into a working customer workflow. Plan the components and permissions, build a small working version, and test setup, everyday use, and recovery before preparing your App Hub submission.

## Selected section

## Map the workflow to app components

An App Hub listing describes the customer solution. Its implementation may combine app types. Keep each component's registration, permissions, and runtime responsibilities explicit.

The **App models** group contains implementation references. **Contact Center solutions** connects those components into a journey for a particular product, starting with BYOVA. **Sandboxes** contains the test-environment guides. Follow the sequence in this page, then open the references your workflow needs.

For example, an embedded app can provide the interface inside Webex while an OAuth integration obtains user-authorized API access. Opening the interface does not grant that API access. A BYOVA solution combines a provider service, Service App authorization, and customer Contact Center configuration; follow its solution guide for that complete journey.

Use the guide for the app type you already selected to define your first milestone:

| Your chosen approach | First working milestone | Implementation guidance |
| --- | --- | --- |
| OAuth integration | A user authorizes the required access and completes one task using the API. | [Integrations](https://developer.webex.com/docs/integrations) and [Authentication](https://developer.webex.com/docs/authentication) |
| Service App | A Full Admin authorizes the app and your service completes one permitted task in the organization. | [Using Webex Service Apps](https://developer.webex.com/app-hub/docs/service-apps); for Contact Center, [Contact Center Service Apps](https://developer.webex.com/docs/contact-center-service-apps) |
| Embedded app | A user opens the app in its intended Webex context and completes one interaction. | [Embedded Apps Developer Guide](https://developer.webex.com/app-hub/docs/embedded-apps-guide) and [Meetings design guidelines](https://developer.webex.com/app-hub/docs/embedded-apps-design-guidelines-for-meetings) |
| Bot | A user can discover how to interact with the bot and complete one useful exchange. | [Bots](https://developer.webex.com/app-hub/docs/bots) |
| Workspace integration | A Full Admin activates the integration and your service completes one intended workspace or device operation. | [Workspace Integrations](https://developer.webex.com/app-hub/docs/workspace-integrations) |
| BYOVA solution | Your provider service connects to a test Contact Center organization and completes a virtual-agent conversation. | [Become a BYOVA Provider](https://developer.webex.com/app-hub/docs/become-a-byova-provider), including its protocol and product prerequisites |

For MCP servers or A2A agents, use the guides for the selected protocol linked from [Choose Your App Hub App Type](https://developer.webex.com/app-hub/docs/choose-your-app-hub-app-type). Confirm their availability and access prerequisites before planning customer testing; beta access is not general availability.
