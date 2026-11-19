---
type: Guide
title: Webex Contact Center MCP Server Beta
display_title: Webex Contact Center MCP Server Beta
canonical_url: https://developer.webex.com/docs/contact-center-mcp-server-beta
content_type: documentation
product_group:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/contact-center-mcp-server-beta)

Use this guide to test the Webex Contact Center MCP Server with a supported MCP client during the Webex Developer Beta. For the complete tool reference, see [Contact Center MCP Server](https://developer.webex.com/docs/contact-center-mcp-server).

## Before you begin

- Ask an organization administrator to enable **Contact Center MCP** in **Control Hub > Apps > Agentic Apps**.
- On the app's **General** tab, confirm the organization policy allows the app. On the **Tools** tab, enable the tools you will test; tools are enabled individually.
- Use a supported MCP client. See the [Webex MCP Server Usage Guide](https://developer.webex.com/docs/webex-agentic-mcp-servers) for supported clients and setup steps.
- Confirm that your user can access the target Webex Contact Center organization and has the permissions required by the tools you will test. Admin configuration tests require an appropriate Contact Center administrator role.

## 1. Select the server and connect

1. Sign in to the Webex Developer Portal, then open the [Contact Center MCP Server](https://developer.webex.com/docs/contact-center-mcp-server) page.
2. Copy the regional server URL shown for your tenant. There is no global server URL.
3. Add the server to your MCP client.
4. Connect with OAuth 2.0, or use a WCIT token from the [Webex agentic token page](https://developer.webex.com/agentic-token). With OAuth, approve only the scopes required for the tools you are testing.
5. Confirm that the client reports the server as connected.

## 2. Run read-only checks first

Run these checks before any write operation:

1. `wxcc-list-flows` — confirm that authorized flows or subflows can be listed or searched.
2. `wxcc-get-flow` — retrieve a draft, latest version, or specific flow version.
3. `wxcc-view-config` — read an authorized configuration resource such as an entry point, team, dial plan, or contact service queue.
4. `wxcc-get-activity-definitions` and `wxcc-describe-activity` — retrieve activity schemas before authoring a flow.
5. `wxcc-get-choices` — resolve organization-specific values instead of guessing IDs.

The expected result is tenant-scoped data for authorized resources only. Stop and report an authorization or data-boundary failure before continuing.

## 3. Test Flow Designer writes safely

1. Use `wxcc-get-flow-template` to retrieve a starter FlowV2 template.
2. Use `wxcc-create-flow` to create an unpublished draft named `MCP_TEST_<date>`.
3. Use `wxcc-save-flow-draft` or `wxcc-patch-flow-draft` to make a small change.
4. Use `wxcc-validate-flow` and confirm validation succeeds before any publish or production action.

Keep the test flow unpublished and do not bind it to a production entry point. Record its name and ID for administrator cleanup.

## 4. Test Contact Center configuration writes

Use `wxcc-admin-config` only with safe test resources such as a test entry point, business hours, dial plan, or dial number. Verify create, update, and delete behavior with a user who has write permission, and verify that an unauthorized user receives a clear failure. Delete each test resource after validation.

## 5. Test real-time subscriptions

1. Use `wxcc-realtime` to discover supported event types.
2. Use `wxcc-realtime` to list existing webhook subscriptions.
3. Use `wxcc-realtime` to create and update a test webhook subscription.
4. Use `wxcc-realtime` to provision a WebSocket session when the client supports it and confirm the response includes a `webSocketUrl` and `subscriptionId`.
5. Use `wxcc-realtime` to delete the test webhook subscription after validation.

## 6. Test historical analytics

1. Run `wxcc-copilot-run-search-query` over a small time range.
2. Compare CSR, ASR, or CLR results with the Contact Center reporting or analytics UI.
3. Confirm that the response contains only data authorized for the target organization.

## Cleanup and rollback

- Do not publish or production-bind the `MCP_TEST_<date>` flow draft.
- Delete test entry points, business hours, dial plans, dial numbers, and webhook subscriptions after validation.
- If a test produces an unexpected write or exposes data outside the target organization, stop testing and report the flow or resource ID, tool name, and error without sharing tokens or customer data.
