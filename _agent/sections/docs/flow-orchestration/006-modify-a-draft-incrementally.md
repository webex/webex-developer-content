---
type: Excerpt
canonical_url: https://developer.webex.com/docs/flow-orchestration
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Modify a draft incrementally
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/flow-orchestration). [Full Markdown](../../../../docs/flow-orchestration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md) [Restrictions](008-restrictions.md)

## Article introduction

Learn how to author a Webex Contact Center flow as a JSON document and import it through the Flow Orchestration APIs — entirely programmatically, without the UI.

## Selected section

## Modify a draft incrementally

Once a draft exists you rarely rewrite the whole document. There are two ways to change it.

### Save a flow draft

Replace the whole draft with the Save Flow Draft operation — `POST …/v2/flows/{flowId}?expectedVersion=N`. Pass `expectedVersion` to enable optimistic locking; the request fails with `409 Conflict` if the flow's version has moved on. Omit it to skip the check. The response is the same metadata envelope as import (`flow`, `preflightWarnings`, `preflightWarningsCount`). Note that a draft save does not increment `flow.version` on its own — `expectedVersion` guards against a published version that has moved on, so repeated saves within the same version are not distinguished by the version number.

### Patch a flow draft

Apply a partial change with the Patch Flow Draft operation — `PATCH …/v2/flows/{flowId}`. The body is a patch contract; the merge happens server-side, is idempotent, and is re-validated, so the draft is never left broken:

```json
{
  "upsert_nodes": [
    {
      "id": "node-hold",
      "name": "HoldMessage",
      "activityType": "action",
      "properties": {
        "activityName": "play-message",
        "prompt": {
          "promptType": "text",
          "text": "Thanks for calling. Please hold.",
          "textType": "text"
        }
      }
    }
  ],
  "upsert_edges": [
    {
      "id": "edge-3",
      "from": "WelcomeMessage",
      "to": "HoldMessage",
      "condition": "out",
      "properties": {}
    }
  ],
  "remove_node_names": [],
  "remove_edge_keys": []
}
```

`upsert_nodes` matches existing nodes by `name` and `upsert_edges` matches by `id` — present items are replaced, new ones are added. `remove_node_names` deletes nodes by `name` and `remove_edge_keys` deletes edges by `id`; if you remove a node, remove the edges that reference it in the same patch or the merged document fails validation. A `PATCH` body may also carry top-level overrides such as `name` and `description`.

This is what makes a hand-authored flow *expandable*: start from the atomic flow above, then grow it one patch at a time.
