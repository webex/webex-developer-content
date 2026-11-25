---
type: Excerpt
canonical_url: https://developer.webex.com/docs/compliance-officer
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Webex Data
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/compliance-officer). [Full Markdown](../../../../docs/compliance-officer.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Compliance Officers can access and manage organization content with dedicated authorization scopes. Learn how data ownership, room permissions, and meeting recordings affect that access.

## Selected section

## Webex Data

### Permissions & Ownership

Data created within Webex belongs to the [organization](https://developer.webex.com/docs/api/v1/organizations) that owns the room (space). The owner of a group room is generally the organization for the person who created the room. For 1:1 rooms between users in different organizations, the organization that each person belongs to owns their participant’s content. Rooms created by bots are owned by the organization of the first non-bot participant.

Data access permissions within Webex vary depending on a few factors: the room creator, room membership, and organization membership. When a room is created, the organization associated with the creator is considered the **owning organization** for the room. If users from other organizations are added to the room, those organizations are **participating organizations** in the room.

In general, the following types of users will be viewing, creating, and managing data within Webex:

- Room participants—can send and view messages within the room.
- Room moderator—users can be assigned as a moderator by a room owner and have exclusive control of the room including the room’s title and participant list.
- Compliance officers for the owning organization—can monitor and manage all data within group rooms created by a member of the organization; can manage all content in 1:1 rooms, including those with external participants.
- Compliance officers for the participating organization-can monitor and manage data created by their users in rooms owned by another organization; can manage all content in 1:1 rooms with external participants.



> **Info**
>
> In a 1:1 room between users of different organizations, either organization’s compliance officers can monitor and manage data created by _both_ participants.



### Security & Privacy

A key management server (KMS) is responsible for the creation and security of the encryption keys the Webex clients use to encrypt and decrypt data and communications. It is architecturally and operationally separated from the rest of the Webex Cloud and its data is not accessible by any other components. Whether the KMS is managed by Cisco or installed and managed on-premise, data within the Webex Cloud is encrypted from end-to-end and is not decrypted until it reaches the API endpoint.

For more information about data security and privacy in Webex, please see the [Webex Security White Paper](https://www.cisco.com/c/dam/en/us/solutions/collateral/collaboration/cloud-collaboration/cisco-spark-security-white-paper.pdf).
