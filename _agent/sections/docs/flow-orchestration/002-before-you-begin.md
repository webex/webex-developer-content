---
type: Excerpt
canonical_url: https://developer.webex.com/docs/flow-orchestration
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Before you begin
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/flow-orchestration). [Full Markdown](../../../../docs/flow-orchestration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Restrictions](008-restrictions.md)

## Article introduction

Learn how to author a Webex Contact Center flow as a JSON document and import it through the Flow Orchestration APIs — entirely programmatically, without the UI.

## Selected section

## Before you begin

You need:

- A Webex Contact Center administrator access token. See [Authentication](https://developer.webex.com/docs/authentication) for how to obtain one.
- Scopes: `cjp:config_read` for the discovery calls, and `cjp:config_write` for validate and import.
- The base URL for your organization's region (see the table below). Webex Contact Center is served from region-specific gateways; use the one your tenant is provisioned in.
- Your organization ID (`{orgId}`) and the project ID (`{projectId}`). The `{orgId}` must be the organization **UUID** (for example `8eb7da9a-c81c-4d13-b08b-38fdeb7330d8`); the Spark-encoded organization ID returned by some generic Webex APIs is not accepted by this gateway. The project ID is a system-generated value that is the same across orgs and environments — always use `5e5c9ad6d61f870d6d778c1b`.

| Region | Base URL |
| --- | --- |
| Integration | `https://api.intgus1.ciscoccservice.com` |

All requests send the token in the `Authorization` header:

```text
Authorization: Bearer <YOUR_ACCESS_TOKEN>
```

The examples below use the shell variables `${TOKEN}` and `${ORG_ID}` for these values, and `${BASE_URL}` for your region's gateway from the table above — for example `export BASE_URL="https://api.intgus1.ciscoccservice.com"`.

### Discover activities

A flow can only reference activities that exist in your project. List them — along with their `group`, input fields, output ports, and the JSON Schema for their inputs — with `listActivityDefinitions`. The response is self-describing and sufficient on its own to construct nodes:

```bash
curl -sS \
  "${BASE_URL}/${ORG_ID}/project/5e5c9ad6d61f870d6d778c1b/v2/activities" \
  -H "Authorization: Bearer ${TOKEN}"
```

Each activity reports an `activityName` and a `group` that classifies it. Read both from the discovery response rather than assuming a fixed set or naming convention — `activityName` values are project-specific and their casing varies (for example `start`, `play-message`, `SetCallerID`, `Feedback-V2`), and `group` is an open set (for example `action`, `terminating-action`, `enum-gateway`). Pick the activities you need by matching on the discovered values:

- **Start** — the activity whose `activityName` is `start`.
- **Play a prompt** — `play-message`.
- **End the flow** — a terminating activity, for example `disconnect-contact`.

To inspect one activity's full input/output/port schema, call `describeActivity` with its `activityName`:

```bash
curl -sS \
  "${BASE_URL}/${ORG_ID}/project/5e5c9ad6d61f870d6d778c1b/v2/activities/play-message" \
  -H "Authorization: Bearer ${TOKEN}"
```

When an input takes a value from a constrained set (a priority, an audio file, a team), resolve the allowed values with `getActivityInputChoices`. Call it with no parameters to list all choices; pass `search=<text>` to filter (type-ahead); add `validate=true` to do a point-lookup of a single value (matched against the choice's `value`/ID, not its display name). For a **cascading** input whose values depend on a sibling input, supply the parent with `parentInputName=<name>` and `parentValue=<value>` — otherwise the call returns `400`. The endpoint is only valid for inputs that expose choices — an input the `describeActivity` definition marks with `allowedValues` or a `choicesEndpoint`; calling it for any other input name returns `400`. Filtering and validation apply to dynamic (`choicesEndpoint`-backed) inputs; a static input (for example `voiceLanguage`) always returns its full enumerated list. Use the exact input name from `describeActivity`:

```bash
curl -sS \
  "${BASE_URL}/${ORG_ID}/project/5e5c9ad6d61f870d6d778c1b/v2/activities/queue-contact/inputs/destination/choices?parentInputName=channelType&parentValue=TELEPHONY" \
  -H "Authorization: Bearer ${TOKEN}"
```

### Discover events

An event flow can only react to events your project exposes. List them with `listEventSpecifications`:

```bash
curl -sS \
  "${BASE_URL}/${ORG_ID}/project/5e5c9ad6d61f870d6d778c1b/v2/event-specifications" \
  -H "Authorization: Bearer ${TOKEN}"
```

Each result's `name` is what you put into an event node's `properties.eventSpecificationName`. Find the global-error event in this list and use its `name` for the event node in [Add a global error handler](https://developer.webex.com/docs/flow-orchestration#add-a-global-error-handler).
