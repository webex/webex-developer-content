---
type: Guide
title: Build for App Hub | Get Started
display_title: Get Started
canonical_url: https://developer.webex.com/docs/app-hub-build-and-test
content_type: documentation
product_group:
- webex-suite
- webex-contact-center
categories:
- app-hub
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/app-hub-build-and-test)

Turn your chosen app type into a working customer workflow. Plan the components and permissions, build a small working version, and test setup, everyday use, and recovery before preparing your App Hub submission.

## Start with one customer workflow

Use this guide after [Choose Your App Hub App Type](https://developer.webex.com/app-hub/docs/choose-your-app-hub-app-type). If you are still exploring App Hub, start with the [Overview](https://developer.webex.com/app-hub/docs/build-for-app-hub).

Write a short development brief before registering components or choosing scopes:

- **Outcome:** What task will the customer complete, and what observable result proves it worked?
- **People:** Who installs or approves the app, who uses it, and who supports it?
- **Context:** Where does the workflow run: your application, a Webex meeting or space, a device workspace, or Contact Center?
- **Access:** Which Webex resources does it need, and whose identity can access them?
- **Prerequisites:** Which Webex products, licenses, roles, and accounts with your service are required?

Keep the first workflow small enough to demonstrate from initial setup through a useful result. Add more features after that path works.

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

## Build a small working version

Work through the selected implementation guide in this order:

1. **Prepare the environment.** Confirm the required products and roles, set up your application or service, and register the components the workflow needs.
2. **Implement authorization.** Use the documented flow for each component and request only the scopes needed for the first workflow. Keep client secrets and refresh tokens on your backend, and exclude credentials from logs.
3. **Connect one real operation.** Replace sample or placeholder behavior with the intended API call, interaction, or conversation. Verify the result in the target Webex context.
4. **Add recovery.** Make denied access, missing prerequisites, expired access, and interrupted setup understandable. Follow the guide for your app type for token renewal and authorization changes.

Keep customer connections separate in your service. When handling a request or event, verify that it uses the intended customer's authorization and resources. If the workflow processes asynchronous events, design retries so they do not repeat an unintended customer action.

## Choose the test environment

Use the [Suite Sandbox](https://developer.webex.com/app-hub/docs/developer-sandbox-guide) for supported Webex Suite workflows or the [Contact Center Sandbox](https://developer.webex.com/app-hub/docs/sandbox_cc) for Contact Center testing. Check each sandbox's prerequisites and available features; access to a sandbox does not enable every API or app type.

Use separate identities for the app developer, customer administrator, and end user when those roles differ. Keep test data separate from customer production data. For BYOVA, also confirm the provider guide's feature and licensing prerequisites for the target organization.

A successful test in your own organization does not prove that another organization can authorize the app. For Service Apps, follow the documented App Hub submission and review path before requesting authorization in another organization. Plan that later validation without assuming the initial private app can perform it.

## Verify the customer journey

Record the setup, expected result, and observed result for each check:

| Check | Evidence to capture |
| --- | --- |
| Initial setup | A person with the intended role can follow your instructions and reach a working connection. |
| Main workflow | The app produces the stated customer result in each Webex context you plan to support. |
| Missing access or prerequisites | The app explains what is missing and provides a useful next step. |
| Expired access or interrupted setup | The documented recovery path restores operation without mixing customer connections. |
| Repeated actions or events | Retries do not produce unintended duplicate customer actions. |
| Removal or deauthorization | The app stops using revoked access; your instructions explain any remaining cleanup and data handling. |

Have someone other than the app's developer follow the setup instructions. Fix any step that depends on undocumented knowledge, an administrator session left open, or credentials copied manually during development.

## Continue to submission and customer setup

You are ready to prepare a submission when you have a working implementation, documented prerequisites and setup instructions, and recorded test results. App Hub review requires the stated features to be operational; a development prototype is not a submission ready for production.

Follow the submission path for your app type. Use [Submit Your App](https://developer.webex.com/app-hub/docs/app-hub-submission-process) for general listing materials, review access, and testing instructions. Embedded apps also use the [Submission Checklist for Embedded Apps](https://developer.webex.com/app-hub/docs/app-hub-submission-checklist-for-embedded-apps). Workspace integrations follow the public integration approval and Control Hub deployment path in [Workspace Integrations](https://developer.webex.com/app-hub/docs/workspace-integrations).

Use [Plan Customer Setup and Authorization](https://developer.webex.com/app-hub/docs/app-hub-customer-onboarding) to turn the tested setup into a repeatable customer process. App registration, listing approval, and customer authorization remain separate steps.
