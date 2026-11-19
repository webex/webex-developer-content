---
type: Excerpt
canonical_url: https://developer.webex.com/docs/flow-orchestration
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Build a custom function
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/flow-orchestration). [Full Markdown](../../../../docs/flow-orchestration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md) [Restrictions](008-restrictions.md)

## Article introduction

Learn how to author a Webex Contact Center flow as a JSON document and import it through the Flow Orchestration APIs — entirely programmatically, without the UI.

## Selected section

## Build a custom function

A **custom function** is a small piece of user-authored code (JavaScript or Python) that a flow can call to transform data — parse a JSON payload, normalize a phone number, look up a value. Functions are managed by the Custom Functions API. Unlike the flow endpoints, its paths are not scoped to a project:

- The base URL is the same regional gateway (`${BASE_URL}`) used for the flow endpoints — see the region table in [Before you begin](https://developer.webex.com/docs/flow-orchestration#before-you-begin).
- Function paths are `/v1/{orgId}/functions…` — there is no `{projectId}` segment.
- Scopes: `cjp:config_read` to list, get, and export; `cjp:config_write` to create, update, test, publish, lock, unlock, and import. The `Authorization: Bearer ${TOKEN}` header is the same as before.

This walkthrough builds a `parseContact` function that takes a contact record and returns the caller's phone digits and area code, then tests and publishes it. Once published, a function can be referenced from a flow.

A function exports a single `handle` entry point. It reads its declared inputs from `request.inputs`, writes its result to `response.data`, and returns the `response`:

```js
export const handle = async (request, response) => {
  const phoneDigits = String(request.inputs.contact.phone).replace(/\D/g, "");
  response.data = {
    phoneDigits,
    areaCode: phoneDigits.slice(0, 3)
  };
  return response;
};
```

### Step 1 — Create the function

`sourceCode` is sent as an escaped string. `inputs[]` declares each input's `name`, `dataType` (one of `boolean`, `datetime`, `decimal`, `integer`, `json`, `string`), and a sample `value`. `outputs` is a stringified JSON object mapping each output name to a sample value. `language` is `js` or `py`. `selectedRuntime` is case-sensitive and defaults to the highest supported runtime for the language (for example `nodejs22.x` for `js`, or `python3.13` for `py`). `timeoutInSec` caps execution time.

```bash
curl -sS -X POST \
  "${BASE_URL}/v1/${ORG_ID}/functions" \
  -H "Authorization: Bearer ${TOKEN}" \
  -H "Content-Type: application/json" \
  --data '{
    "name": "parseContact",
    "description": "Parses a contact record: strips the phone to digits and extracts the area code.",
    "language": "js",
    "selectedRuntime": "nodejs22.x",
    "timeoutInSec": 3,
    "sourceCode": "export const handle = async (request, response) => {\n  const phoneDigits = String(request.inputs.contact.phone).replace(/\\D/g, \"\");\n  response.data = { phoneDigits, areaCode: phoneDigits.slice(0, 3) };\n  return response;\n};",
    "inputs": [
      {
        "name": "contact",
        "dataType": "json",
        "value": "{\"name\":\"John Doe\",\"phone\":\"(415) 555-0132\"}"
      }
    ],
    "outputs": "{\"phoneDigits\":\"4155550132\",\"areaCode\":\"415\"}"
  }'
```

A successful create returns `201 Created`. The source code is returned under `fnCode` and the server-side metadata — including the assigned `id` and a `Draft` status — under `fnMetadata`:

```json
{
  "fnCode": "export const handle = async (request, response) => {\n  const phoneDigits = String(request.inputs.contact.phone).replace(/\\D/g, \"\");\n  response.data = { phoneDigits, areaCode: phoneDigits.slice(0, 3) };\n  return response;\n};",
  "fnMetadata": {
    "id": "64f1b2c3d4e5f6a7b8c9d0e1",
    "orgId": "8eb7da9a-c81c-4d13-b08b-38fdeb7330d8",
    "name": "parseContact",
    "description": "Parses a contact record: strips the phone to digits and extracts the area code.",
    "language": "js",
    "selectedRuntime": "nodejs22.x",
    "status": "Draft",
    "timeoutInSec": 3,
    "tagVersionMap": {},
    "lockedBy": "",
    "createdBy": "user@example.com",
    "createdDate": "2026-01-15T09:12:00.000Z",
    "lastModifiedBy": "user@example.com",
    "lastModifiedDate": "2026-01-15T09:12:00.000Z"
  }
}
```

### Step 2 — Test it

Run the function with a test payload. `inputs` is a JSON object whose keys match the declared input names — here, the John Doe contact:

```bash
curl -sS -X POST \
  "${BASE_URL}/v1/${ORG_ID}/functions/64f1b2c3d4e5f6a7b8c9d0e1:test" \
  -H "Authorization: Bearer ${TOKEN}" \
  -H "Content-Type: application/json" \
  --data '{
    "inputs": {
      "contact": {
        "name": "John Doe",
        "phone": "(415) 555-0132"
      }
    }
  }'
```

The response carries the function's `response.data` in `data`, along with the HTTP `statusCode`, an `errorMessage` (empty on success), and the execution time in `timeTakenInMilliseconds`:

```json
{
  "statusCode": 200,
  "data": {
    "phoneDigits": "4155550132",
    "areaCode": "415"
  },
  "errorMessage": "",
  "timeTakenInMilliseconds": 12
}
```

The test call implicitly publishes the latest draft before running, so it always executes your most recent source code.

### Step 3 — Publish it

Publish the draft under one or more tags (`Dev`, `Test`, `Latest`, `Live`) to make a version addressable:

```bash
curl -sS -X POST \
  "${BASE_URL}/v1/${ORG_ID}/functions/64f1b2c3d4e5f6a7b8c9d0e1:publish" \
  -H "Authorization: Bearer ${TOKEN}" \
  -H "Content-Type: application/json" \
  --data '{ "tags": ["Live"], "comment": "Initial release." }'
```

Publishing returns the same `{ "fnCode", "fnMetadata" }` envelope, with the new tag reflected in `fnMetadata.tagVersionMap`. The published function can now be referenced from a flow.

### Function lifecycle reference

The rest of the lifecycle follows the same pattern:

- `GET …/v1/{orgId}/functions` and `GET …/v1/{orgId}/functions/{id}` — list and inspect.
- `PUT …/v1/{orgId}/functions/{id}` — update the draft (same body shape as create).
- `…/v1/{orgId}/functions/{id}:export` returns the function definition as a JSON object (`name`, `language`, `runtime`, `description`, `sourceCode`, `inputs`, `outputs`), and `…/v1/{orgId}/functions:import` accepts that JSON object as a multipart file upload — together they move a function between environments.
- `…/v1/{orgId}/functions/{id}:lock` and `:unlock` coordinate concurrent edits; each returns the JSON string `"OK"`.
