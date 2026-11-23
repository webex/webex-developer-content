---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-assistant-skills-reference-guide
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Request Payload
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

## Request Payload

After decrypting the message received from the **Assistant skills** service, the request body will look as follows:
```json
{
  "text": "hello",
  "context": {
    "orgId": "00000000-0000-0000-0000-000000000000",
    "userId": "00000000-1111-1111-1111-000000000000",
    "userType": null,
    "developerDeviceId": "00000000-2222-2222-2222-000000000000",
    "supportedDirectives": [
      "speak",
      "ui-hint",
      "clear-web-view",
      "asr-hint",
      "reply",
      "display-web-view",
      "listen",
      "sleep",
      "assistant-event"
    ]
  },
  "params": {
    "target_dialogue_state": null,
    "time_zone": "America/Los_Angeles",
    "timestamp": 1638833645,
    "language": "en",
    "locale": "en_US",
    "dynamic_resource": {},
    "allowed_intents": []
  },
  "frame": {},
  "challenge": "4f1cf832c0affcfb31afc841ca9fab2cd8243811131d37966ce2beba65d9a99d"
}
```

- ``text``: This is the **Actor**'s query. This can sometimes be empty when the **Actor** asks to speak to the skill without a query.
- ``context``: Contains relevant and potentially useful information about the user making the query.
    - ``orgId``: A UUID of the organization who the **Actor** is registered to.
    - ``userId``: A UUID of the **Actor** themself if available.
    - ``userType``: A string value of which type of account making the request if available.
    - ``developerDeviceId``: A UUID of the device used to make the query.
    - ``supportedDirectives``: A list of directives that are allowed from your skill. More directive details are available below. 
- ``params``: Contains information specific to MindMeld powered applications but some values maybe useful for your skill. Additional information can be found in the [MindMeld documentation](https://www.mindmeld.com/docs/userguide/dm.html?highlight=params#params).
    - ``target_dialogue_state``: The name of the dialogue handler that you want to reach in the next turn. One particular case, `skill_intro` must be supported. If the `target_dialogue_state` is `skill_intro`, the skill should return an introductory message.
    - ``time_zone``: The name of IANA time zone.
    - ``timestamp``: A valid 13-digit unix timestamp representation.
    - ``language``: A valid ISO 639 two letter code for the language used to make the query.
    - ``locale``: A valid ISO 3166-2 locale code. Locale codes are represented as ISO 639-1 language code and ISO3166 alpha 2 country code separated by an underscore character.
    - ``dynamic_resource``: A dictionary containing data used to influence the language classifiers by adding resource data for the given turn (see dynamic gazetteer documentation).
    - ``allowed_intents``: A list of intents that you can set to force the language processor to choose from.
- ``frame``: A mutable object that contains information that is preserved during multiple interactions with the skill. 
- ``challenge``: A uniquely generated string that the **Assistant skills** service includes in each request and is used to verify that the skill was able to decrypt the payload. The `challenge` is then expected to be sent back in the response to the service. If the `challenge` is missing or incorrect, the service will return an error to **Assistant NLP**.
