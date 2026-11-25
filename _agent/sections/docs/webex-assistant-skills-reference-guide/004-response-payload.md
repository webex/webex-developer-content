---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-assistant-skills-reference-guide
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Response Payload
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-assistant-skills-reference-guide). [Full Markdown](../../../../docs/webex-assistant-skills-reference-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

We will go over the structure of the requests sent to your Skill from the **Assistant Skills** service and the
responses expected to be returned from your Skill.

---



> **Warning**
>
> No new features are being added to Webex Assistant Skills and only skills added through May 2025 are directly supported by Cisco.

## Selected section

## Response Payload

Next, we'll go over the expected structure of the response from your Skill. The response should include `directives` and a `challenge`, expressed in JSON.

- ``directives``: A list of `directive` objects that will instruct the **Assistant** on what actions to perform and what views to display.
- ``challenge``: A uniquely generated string originally sent from the **Assistant skills** service that must be returned in order to authenticate the response.

```json
{
  "directives": [
    {
      "name": "reply",
      "type": "view",
      "payload": {
        "text": "This is the echo skill. Say something and I will echo it back."
      }
    },
    {
      "name": "speak",
      "type": "action",
      "payload": {
        "text": "This is the echo skill. Say something and I will echo it back."
      }
    },
    {
      "name": "listen",
      "type": "action",
      "payload": {}
    }
  ],
  "challenge": "520d1c22c9c33ed169997d62da855e60145320767f49a502270fee0e7fb59ff1"
}
```
