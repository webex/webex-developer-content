---
type: Guide
title: Manage Your Published App
display_title: Manage Your Published App
canonical_url: https://developer.webex.com/docs/manage-your-published-app
content_type: documentation
product_group:
- webex-suite
- webex-contact-center
categories:
- app-hub
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/manage-your-published-app)

Keep your App Hub listing accurate, support customers through changes, and plan updates or retirement alongside the authorization lifecycle of your app.

## Establish a maintenance baseline

After your app is approved, keep a record of its Developer Portal app ID, App Hub listing URL, registered components, supported Webex contexts, and review correspondence. Identify the people responsible for the application, customer support, and App Hub review requests.

Keep credentials in your approved secrets store, separate from listing and support records. Never put client secrets, access tokens, refresh tokens, or customer data in an App Hub description or support request.

The [App Hub submission guide](https://developer.webex.com/docs/app-hub-submission-process) defines the listing and review requirements. Continue to meet the requirements that apply to your app after publication.

## Keep your listing accurate

Review your listing whenever the customer experience changes. Check that:

- The description, screenshots, and supported Webex contexts match the released app.
- Setup instructions explain required accounts, licenses, permissions, and administrator actions.
- Pricing information and links reflect your current offering.
- The landing page, privacy information, support links, and contact details remain reachable.
- The listing does not advertise functionality that customers cannot use.

For listing edits or questions about review, reply through your existing App Hub review correspondence. If you cannot access that thread, contact [Webex Developer Support](https://developer.webex.com/support) with your app ID, listing URL, and the requested change. Ask the review team which update process applies to your app type.

Check the [multiple submission guidelines](https://developer.webex.com/docs/app-hub-submission-process#multiple-submission-guidelines) before creating another listing for an existing product. Additional components or Webex contexts do not automatically require separate listings.

## Plan application and permission changes

Before releasing a change, compare it with the behavior and permissions customers previously approved. Treat these as separate work items:

1. **Your application:** Test the new behavior and prepare a recovery or rollback plan.
2. **Your registration and customer authorization:** Follow the app-type guide for configuration, scopes, credentials, and authorization changes. Do not assume existing grants include new permissions.
3. **Your App Hub listing:** Update affected descriptions and customer instructions through the review team. Ask whether the change requires another review before scheduling the release.

These steps can have different owners and completion times. A listing update does not grant API permissions, and an application deployment does not prove that an App Hub update has been reviewed.

Use the relevant guidance:

- [Integrations](https://developer.webex.com/docs/integrations) and [Authentication](https://developer.webex.com/docs/authentication) for user-authorized access.
- [Service Apps](https://developer.webex.com/docs/service-apps) for administrator authorization and organization-specific credentials.
- [Embedded Apps Developer Guide](https://developer.webex.com/docs/embedded-apps-guide) for embedded configuration, privacy, and supported contexts.
- [Workspace Integrations](https://developer.webex.com/docs/workspace-integrations) for workspace integration changes and activation.
- [Admin Approval Guide for Agentic Apps](https://developer.webex.com/docs/admin-approval-guide-for-agentic-apps) for server and tool review, signature changes, and post-approval monitoring.

## Support customers throughout the lifecycle

Provide customers with a support path for your application and distinguish application issues from Webex platform issues. For a platform investigation, include the affected workflow, time and timezone, error details, and available request or tracking identifiers. Share only the information needed to investigate; remove credentials and unnecessary personal data.

Test recovery for expired credentials, declined authorization, interrupted setup, and unavailable dependencies. Use the [Authentication](https://developer.webex.com/docs/authentication) and [Service Apps](https://developer.webex.com/docs/service-apps) guides for the relevant credential flow, and [Webhooks](https://developer.webex.com/docs/webhooks) for event-driven workflows.

For BYOVA, follow [Maintain the DataSource Connection](https://developer.webex.com/docs/become-a-byova-provider#maintain-the-datasource-connection) and [Handle Deauthorization and Offboarding](https://developer.webex.com/docs/become-a-byova-provider#handle-deauthorization-and-offboarding). Keep each customer's authorization and provisioning state separate.

Monitor the [API Changelog](https://developer.webex.com/docs/api/changelog) and [API and SDK Support Policy](https://developer.webex.com/docs/webex-api-and-sdk-support-policy) for changes that affect your dependencies. Test relevant updates before customers reach a migration deadline.

## Coordinate ownership changes

Before a responsible person leaves or your company changes ownership, identify who will maintain the app, receive review correspondence, operate the service, and support existing customers.

Contact the App Hub review team through your existing correspondence, or [Developer Support](https://developer.webex.com/support), to confirm the supported process for changing the listing contact or registration ownership. Include the app ID, listing URL, current organization, requested change, and an authorized contact. Do not send credentials or assume that creating a replacement registration transfers existing customer authorizations.

Once the agreed change is complete, verify that the designated people can access the required management tools and receive support and review communications.

## Plan retirement and customer offboarding

Plan the customer transition before stopping the service:

1. Identify affected customers, dependencies, and any data export or deletion work required by your commitments to them.
2. Communicate the planned end of service, any replacement, required customer actions, and the support path.
3. Coordinate the App Hub listing change or removal with the review team through your existing correspondence or [Developer Support](https://developer.webex.com/support).
4. Complete the deauthorization, deprovisioning, and data-handling steps for your app type.
5. Verify that your application no longer performs work for offboarded customers and that their provisioning state reflects the change.

Listing removal, Webex authorization, and your own service's customer state are separate concerns. Confirm each explicitly rather than assuming that removing a listing revokes credentials or deletes customer data.

For Service Apps, use [Deauthorizing a Service App](https://developer.webex.com/docs/service-apps#deauthorizing-a-service-app). For BYOVA, use the provider guide's [offboarding procedure](https://developer.webex.com/docs/become-a-byova-provider#handle-deauthorization-and-offboarding). Follow the applicable product guide for other app types.

## Verify the result

After an update, ownership change, or retirement, check the resulting customer experience:

- The App Hub listing reflects the agreed change.
- Published setup and support links work for the intended audience.
- New and existing customers see the expected application behavior.
- Authorization and offboarding behavior match the selected app type.
- Your operational and support owners have the information needed to maintain the result.
