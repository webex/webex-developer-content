---
type: Excerpt
canonical_url: https://developer.webex.com/docs/desktop-sdk-reference
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Methods and Properties
- Agent State and Availability
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/desktop-sdk-reference). [Full Markdown](../../../../docs/desktop-sdk-reference.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Find Desktop SDK modules, methods, properties, and events with links to their detailed reference pages.

## Parent context

## Methods and Properties

Each link opens the parameters, examples, responses, and restrictions for that API member. Deprecation notes identify legacy APIs; use the documented replacement where one is available.

## Selected section

### Agent State and Availability

| API member | Purpose | Status |
| --- | --- | --- |
| [fetchPaginatedAuxCodes](https://developer.webex.com/docs/desktop-agent-state#fetchpaginatedauxcodes) | Retrieves the current idle codes or the current wrap up codes. | — |
| [getIdleCodes()](https://developer.webex.com/docs/desktop-agent-state#getidlecodes) | Retrieves the current idle codes. | Deprecated; use fetchPaginatedAuxCodes |
| [getWrapUpCodes()](https://developer.webex.com/docs/desktop-agent-state#getwrapupcodes) | Retrieves the wrap up codes. | Deprecated; use fetchPaginatedAuxCodes |
| [getMediaTypeQueue(mediaType)](https://developer.webex.com/docs/desktop-agent-state#getmediatypequeuemediatype) | Retrieves the current media queue for one channel type. | — |
| [latestData](https://developer.webex.com/docs/desktop-agent-state#latestdata) | Fetches the latest user related information. | — |
| [stateChange(state, auxCodeIdArray)](https://developer.webex.com/docs/desktop-agent-state#statechangestate-auxcodeidarray) | Changes the state of an agent. | Deprecated; use stateChangeV2 |
| [stateChangeV2(channelType, state, auxCodeId, reason, agentId)](https://developer.webex.com/docs/desktop-agent-state#statechangev2channeltype-state-auxcodeid-reason-agentid) | Changes the state of a particular channel for the agent. | — |
| [addEventListener](https://developer.webex.com/docs/desktop-agent-state#addeventlistener) | Listens to an event named **updated** that is logged if the dn, status, or subStatus field is changed. | — |
