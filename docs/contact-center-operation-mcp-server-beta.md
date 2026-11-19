---
type: Guide
title: Webex Contact Center Operation MCP Server Beta
display_title: Webex Contact Center Operation MCP Server Beta
canonical_url: https://developer.webex.com/docs/contact-center-operation-mcp-server-beta
content_type: documentation
product_group:
- webex-contact-center
categories:
- create
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/contact-center-operation-mcp-server-beta)

Use this guide to test the Webex Contact Center Operation MCP Server with a supported MCP client during the Webex Developer Beta. For the complete tool reference, see [Contact Center Operation MCP Server](https://developer.webex.com/docs/contact-center-operation-mcp-server).

## Before you begin

The Webex Contact Center Operation MCP Server brings Webex Contact Center operational data and configuration into AI assistants. During the beta, the server helps teams investigate Contact Center operations using natural-language questions grounded in data from their Webex Contact Center organization.

This beta is currently offered as a standalone MCP server that connects to supported AI assistant clients. A future release will bring this capability into the desktop AI Assistant.

The Operations MCP is read-only. It can retrieve and explain Webex Contact Center operational information, but it does not create, update, publish, or delete Contact Center configuration, flows, or subscriptions.

To participate in the beta:

1. Sign up through the [Webex Developer Beta Program](https://developer.webex.com/docs/webex-developer-beta-program).
2. Complete the participation survey shared with your beta invitation or Cisco beta contact.

Your organization administrator must enable the MCP server in Webex Control Hub before it can be used.

## 1. Prepare the organization

Ask your Webex organization administrator to:

1. Open **Control Hub > Apps > Agentic Apps**.
2. Enable Contact Center MCP for the organization.
3. On the **General** tab, confirm that the organization policy allows the app.
4. On the **Tools** tab, enable only the approved Operations MCP tools included in your beta test.
5. Confirm that your test user can access the target Webex Contact Center organization.
6. Confirm that the test user has the Contact Center permissions needed for the checks.

Use test data or approved operational data. Tool results can contain customer conversation content, contact identifiers, agent activity, and routing details. Use only an approved MCP client, and do not include customer information in screenshots or test reports unless it is required and approved.

## 2. Connect the Operations MCP

1. Sign in to the Webex Developer Portal.
2. Open the [Contact Center Operation MCP Server](https://developer.webex.com/docs/contact-center-operation-mcp-server) page.
3. Copy the regional server URL shown for your tenant. There is no single global server URL.
4. Add the server to your supported MCP client.
5. Connect using OAuth 2.0, or use a Webex Client Identity Token (WCIT) when your MCP client supports elicitation. Clients without elicitation support must use OAuth 2.0. See [Connect Webex MCP Servers to External Clients](https://developer.webex.com/docs/webex-agentic-mcp-servers).
6. With OAuth 2.0, create or update your Webex Integration with `spark:mcp`, `cjp:config_read`, and `spark:people_read`. Add `cjp:user` only if your approved beta scope includes `wxcc-operations-get-va-summary` or `wxcc-operations-get-va-transcript`. With WCIT, the initial token includes only `spark:mcp`; clients that support elicitation request `cjp:config_read`, `spark:people_read`, and `cjp:user` only when a tool needs them.
7. Confirm that the client shows the server as connected.

If you use OAuth 2.0, record the client ID once and store the client secret only in the MCP client's secure secret storage. Never record or share a client secret, WCIT token, access token, or refresh token in screenshots, notes, or test reports.

Record the client name and version, region, date, user role, and enabled tools. Test Virtual Agent summary or transcript tools only when the organization, user, and approved beta scope allow that access.

The tools displayed by the connected beta server are the source of truth for that test environment. Tools can be enabled individually, so run only the checks for tools that are visible and approved.

### Connection pass criteria

- The regional server URL is accepted.
- Authentication completes successfully.
- The client reports the Operations MCP as connected.
- The approved Operations tools are visible.
- No unapproved write capability is presented as part of the Operations MCP test.

Stop testing and report the problem if the server cannot connect, the wrong regional URL is shown, or the available tools do not match the approved beta scope.

## 3. Run basic read-only checks

Run these checks first using a known test organization and, where possible, a known test object.

| Check | Operations MCP tool | What to do | Expected result |
|---|---|---|---|
| Organization overview | `wxcc-operations-describe-org` | Ask for a high-level Contact Center overview. | The response describes only the authorized organization and clearly labels counts or samples. |
| Metric discovery | `wxcc-operations-describe-metrics` | Ask which fields and metrics are available for a report. | The response identifies supported fields instead of guessing. |
| Schema check | `wxcc-operations-validate-schema` | Run when a report or Search query may be affected by a field or schema issue. | The result clearly says whether validation succeeded, found a difference, or could not complete. |
| Configuration list | `wxcc-operations-list-config` | List one approved resource such as a queue, team, site, entry point, skill, or user. | Only authorized configuration is returned. |
| Configuration detail | `wxcc-operations-get-config-object` | Retrieve one known object by ID. | The requested object is returned without changing it. |
| Configuration references | `wxcc-operations-get-configuration-references` | Find objects that refer to one known configuration object. | References are limited to the authorized organization and clearly identified. |

### Basic pass criteria

- The response contains only authorized organization data.
- Counts, returned rows, and any limits are explained clearly.
- A missing object is not reported as definitively absent when the search was incomplete.
- No configuration changes occur.
- The client identifies the tool used or makes the result traceable to the test.

## 4. Test configuration and routing visibility

Use known test objects where possible. These checks read the current Contact Center configuration; they do not change it.

| Check | Operations MCP tool | What to validate |
|---|---|---|
| List flows | `wxcc-operations-list-flows` | Authorized flows and subflows can be listed or searched. |
| Read a flow | `wxcc-operations-export-flow` | A known flow can be retrieved for review. |
| Queue routing | `wxcc-operations-explain-queue-routing` | A known queue's routing settings, skill requirements, related flow references, and bounded configured-agent coverage when requested are explained. |
| Agents by skill | `wxcc-operations-get-agents-by-skill` | The response identifies configured coverage for a known skill and distinguishes configuration from current availability. |
| AI feature settings | `wxcc-operations-get-ai-features` | The response shows the tenant's configured Cisco AI Assistant feature state and scope, subject to reported coverage. |

For a queue-routing test, record the queue used and confirm that the response does not confuse an agent being logged in or available with being qualified for the queue.

### Routing pass criteria

- The requested queue, flow, skill, or feature is identified correctly.
- The response distinguishes configured settings from what happened to a live contact.
- Related flows and references are clearly labeled.
- Partial or unavailable information is identified instead of being presented as complete.

## 5. Test reporting and historical analytics

Use a short, agreed time window and the same time zone when comparing results with another Webex Contact Center report or dashboard.

| Check | Operations MCP tool | What to validate |
|---|---|---|
| Contact reporting | `wxcc-operations-generate-report` | Contact, queue, and contact-leg results use the requested time range and reporting definition. |
| Agent reporting | `wxcc-operations-generate-agent-report` | Agent metrics use the selected agents, interval, time zone, and grouping. |
| Custom Search | `wxcc-operations-run-search-query` | A small custom query returns only authorized historical data. Use this when the typed reports cannot answer the question. |
| Agent activity | `wxcc-operations-get-agent-activity` | A known agent's activity is returned for the selected time window. |

Before comparing numbers, record:

- The time range and time zone.
- The report or record type.
- The filters and grouping.
- Whether the result is at contact, contact-leg, human-agent session, agent activity, or interval level.
- The expected count or result from the comparison view.

### Reporting pass criteria

- The tool uses the requested time window and filters.
- The result states what the number represents.
- The result distinguishes returned rows from the total number of matching records.
- A partial, delayed, or unavailable result is identified.
- The client does not claim that a failed query means there were zero records.

## 6. Test one contact and related artifacts

Use an approved test contact or task ID. Do not include the customer's phone number, address, transcript, or other sensitive content in the test report.

| Check | Operations MCP tool | What to validate |
|---|---|---|
| Contact journey | `wxcc-operations-get-contact-timeline` | The contact's arrival, IVR, queue, agent, transfer, hold, wrap-up, and termination events are shown in order when available. |
| Contact summaries | `wxcc-operations-get-contact-summaries` | An AI-generated contact summary is returned for the approved contact when available. |
| Recording metadata | `wxcc-operations-list-recordings` | Recording and transcript metadata is listed for the approved contact. |
| Virtual Agent summary | `wxcc-operations-get-va-summary` | The approved contact's Virtual Agent handoff or reconnect summary is returned when available and authorized. |
| Virtual Agent transcript | `wxcc-operations-get-va-transcript` | The approved contact's Virtual Agent transcript is returned when available, authorized, and the tenant has the required entitlement. |

Operations MCP recording checks are metadata checks. They are not a test of playing, downloading, or streaming call or screen recordings. Virtual Agent transcript text is a separate capability and should be tested only with approved contacts, the `cjp:user` scope, and the required entitlement.

### Contact pass criteria

- The selected contact or task is the one being tested.
- Events are presented in chronological order when available.
- Contact-level, session-level, and leg-level information is not mixed without explanation.
- Missing, delayed, or partial artifacts are identified.
- No recording media or unnecessary customer content is exposed.

## 7. Test AI Agent Studio information

Use an approved AI Agent and session if your beta scope includes these tools.

AI Agent Studio tools return configured-agent, session, message, and audit evidence.

| Check | Operations MCP tool | What to validate |
|---|---|---|
| List AI Agents | `wxcc-operations-list-ai-agents` | Authorized AI Agents can be listed. |
| List sessions | `wxcc-operations-list-ai-agent-sessions` | Sessions for one authorized AI Agent can be listed for the selected view. |
| Read one session | `wxcc-operations-get-ai-agent-session` | One known session can be retrieved. |
| Read messages | `wxcc-operations-get-ai-agent-session-messages` | Messages can be counted or returned within the approved limit. |
| Audit an AI Agent | `wxcc-operations-audit-ai-agent` | The selected scope returns a redacted configuration view or bounded evidence from one exact session or up to three recent sessions. |

Do not confuse AI Agent Studio sessions with Contact Center Search analytics, Virtual Agent transcripts, or a contact's ordinary task record.

### AI Agent pass criteria

- The correct AI Agent and session are selected.
- Results are limited to the authorized organization.
- Message results remain within the agreed scope and limit.
- AI Agent Studio evidence is not presented as Contact Center Search analytics.
- Audit findings state their sample and coverage limits and do not label no-tool or ungrounded turns as confirmed hallucinations.
- The response clearly identifies when no session or message data is available.

## 8. Test access control and failure handling

Use administrator-approved test accounts or test conditions:

- A user without Contact Center access attempts a read-only check.
- A user with limited permissions attempts to read an unavailable resource.
- An invalid flow, object, contact, agent, session, or task ID is supplied.
- A report uses an invalid or reversed time range.
- A Search query uses an unsupported field or record type.
- An authorization expires or is revoked.

Expected behavior:

- The request fails clearly and safely.
- No unauthorized data is returned.
- No write occurs.
- The message explains the next action, such as correcting the input or requesting access.
- The error does not expose tokens, secrets, or unrelated customer data.

## 9. Beta acceptance checklist

Mark the test **Pass** only when all applicable items are true:

- [ ] The administrator enabled Contact Center MCP and the approved Operations tools.
- [ ] The regional server connected successfully to the supported MCP client.
- [ ] Organization and configuration checks returned only authorized data.
- [ ] Routing and flow information was understandable and read-only.
- [ ] Reports used the agreed time range, time zone, filters, and data level.
- [ ] A known contact could be traced when the required data was available.
- [ ] Recording results remained metadata-only.
- [ ] Virtual Agent and AI Agent information was tested only with approved access.
- [ ] Invalid or unauthorized requests failed clearly.
- [ ] No data outside the target organization was returned.
- [ ] No configuration, flow, or subscription was changed.
- [ ] The test report contains no access tokens, secrets, or unnecessary customer information.

## 10. Beta test report template

| Item | What to record |
|---|---|
| Test date and time | Include the time zone. |
| Organization and region | Use the approved organization and regional server. |
| MCP client | Client name and version, if visible. |
| User access | Tester role, such as administrator, supervisor, or read-only user. |
| Tool | The Operations MCP tool used. |
| Test | Short description of the question or read-only action. |
| Expected result | What should have happened. |
| Actual result | What happened, including success or failure. |
| Test object | Use a test queue, flow, contact, agent, or session ID when applicable. |
| Evidence | Sanitized screenshot or error text. Never include a token, recording URL, transcript, or unnecessary customer content. |
| Cleanup/status | Confirm that no change was made and note any follow-up needed. |

## 11. Report a problem

Stop and report the issue when:

- The server cannot connect after the administrator confirms setup.
- A read-only tool returns data outside the target organization.
- A read-only tool changes configuration or operational data.
- A permitted request fails unexpectedly.
- An unauthorized request succeeds.
- A report gives a result that cannot be explained using the same time range, filters, and data level.
- A recording check exposes media instead of approved metadata.
- A Virtual Agent or AI Agent result exposes information outside the approved test.

Include the tool name, date and time with time zone, region, user role, expected result, actual result, sanitized error message, and test object ID if one was used. Do not send access tokens, refresh tokens, recording URLs, transcripts, or unnecessary customer information.

To share feedback, ask questions, or report issues, use the beta feedback channel shared with your beta invitation or Cisco beta contact.
