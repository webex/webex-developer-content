---
type: Excerpt
canonical_url: https://developer.webex.com/docs/virtual-agent-transcripts-and-call-summary
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Server host details
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/virtual-agent-transcripts-and-call-summary). [Full Markdown](../../../../docs/virtual-agent-transcripts-and-call-summary.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](001-prerequisites.md)

## Article introduction

---

This document describes how a custom widget in the WxCC agent desktop, or a third-party custom desktop, can interact with the Serving API service. This interaction allows the retrieval of Virtual Agent transcripts and the Virtual Agent transfer summary when a call is transferred from a virtual agent to a human agent.

## Selected section

## Server host details

To retrieve the server details:

1. Construct the following REST request:

    - `URL`: <https://u2c.wbx2.com/u2c/api/v1/user/catalog>
    - `Method`: GET
    - `Query Params`:

        | Parameter  | Value               |
        | ---------- | ------------------- |
        | `types`    | `WCC`               |
        | `services` | `wccai-serving-api` |

1. Add an `Authorization` header.

    **Example**: `Authorization: Bearer <access_token>`

1. Execute the REST request.

Here's an example response:

```json
{
  "services": [
     {
     "serviceName": "wccai-serving-api",
     "logicalNames": [
       "https://serving-api-streaming.wxcc-us1.cisco.com:443"
      ],
     "serviceUrls": [
        {
          "baseUrl": "https://serving-api-streaming.wxcc-us1.cisco.com:443",
          "priority": 5
        }
     ],
     "internalServiceUrls": [],
      "ttl": -1,
     "id": "urn:WCC:US1:wccai-serving-api"
   }
  ],
 "format": "servicelist"
}
 ```
