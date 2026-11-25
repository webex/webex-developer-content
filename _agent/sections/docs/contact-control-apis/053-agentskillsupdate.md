---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-control-apis
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- AgentSkillsUpdate
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-control-apis). [Full Markdown](../../../../docs/contact-control-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Registering for Websocket Connection](002-registering-for-websocket-connection.md) [Common Payload Fields](003-common-payload-fields.md)

## Article introduction

---

# Contact Control APIs

When invoking the following Contact Control APIs, it is important to know that they are asynchronous and may return any of the notification payloads in this guide at any point.

## Selected section

## AgentSkillsUpdate
This is triggered when an agent’s skills are updated after a skill profile or skill assignment change.

For common payload fields, refer to [Common Payload Fields](https://developer.webex.com/docs/contact-control-apis#common-payload-fields).

<details>
<summary  style="cursor: pointer;">Click to see Event Payload details.</summary>

| **Field**                 | **Description**                                                                       |
|---------------------------|---------------------------------------------------------------------------------------|
| `skillProfileId`          | Identifier of the skill profile currently associated with the agent, when applicable. |
| `skillProfileName`        | Name of the skill profile currently associated with the agent, when applicable.       |
| `skillProfileLevel`       | Level at which the skill profile is applied. Example values: `User`, `Team`.          |
| `skills`                  | List of skills currently associated with the agent after the update.                  |
| `skills[].skillId`        | Unique identifier of the skill.                                                       |
| `skills[].skillName`      | Display name of the skill.                                                            |
| `skills[].skillType`      | Type of skill value. Example values: `boolean`, `text`, `proficiency`, `enum`.        |
| `skills[].skillValue`     | Value currently assigned for the skill.                                               |
| `skills[].agentId`        | Unique identifier of the agent associated with the skill entry.                       |
| `skills[].isDynamicSkill` | Indicates whether the skill entry came from a dynamic skill assignment.               |
| `dialNumber`              | Agent dial number associated with the current session, when available.                |

</details>

```json
{
  "eventType": "AgentDesktopMessage",
  "orgId": "org-id-1",
  "agentId": "agent-id-1",
  "trackingId": "tracking-id-1",
  "skillProfileId": "skill-profile-id-1",
  "skillProfileName": "Skill Profile Name",
  "skillProfileLevel": "User-level",
  "agentSessionId": "agent-session-id-1",
  "skills": [
    {
      "skillId": "skill-id-1",
      "skillName": "Skill Name 1",
      "skillType": "boolean",
      "skillValue": "1",
      "agentId": "agent-id-1",
      "isDynamicSkill": false
    },
    {
      "skillId": "skill-id-2",
      "skillName": "Skill Name 2",
      "skillType": "boolean",
      "skillValue": "1",
      "agentId": "agent-id-1",
      "isDynamicSkill": false
    }
  ],
  "dialNumber": "1000000000",
  "eventTime": 1700000000000,
  "type": "AgentSkillsUpdate"
}
```
