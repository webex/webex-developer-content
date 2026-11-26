---
type: Excerpt
canonical_url: https://developer.webex.com/docs/meetings
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Creating and Using Webex Apps
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/meetings). [Full Markdown](../../../../docs/meetings.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Meetings API Scopes](003-meetings-api-scopes.md) [User Level Authentication and Scopes](004-user-level-authentication-and-scopes.md) [Admin/Organization Level Authentication and Scopes](005-admin-organization-level-authentication-and-scopes.md) [Group Level Authentication and Scopes](006-group-level-authentication-and-scopes.md) [Compliance Officer Level Authentication and Scopes](007-compliance-officer-level-authentication-and-scopes.md) [Scopes and User Roles](008-scopes-and-user-roles.md) [Warnings](014-warnings.md) [Restrictions on Updating a Meeting](015-restrictions-on-updating-a-meeting.md)

## Article introduction

The new Webex Meetings REST API enables seamless integration of Webex Meetings into your websites, apps, and services. Schedule meetings, invite meeting attendees, update preferences, and more.

---



> **Warning**
>
> **XML API Deprecation Announcement**  
> The Meetings-related XML APIs will be deprecated and the End-of-Support (EoS) date is planned for the second half of 2023. Cisco will continue to resolve bugs up to this date, but new features will only be implemented for the REST APIs suite. The End-of-life (EoL) timeframe for Meetings-related XML APIs is targeted for **March 31, 2024**, at which time the APIs will be retired. For more information on how to migrate from XML to REST APIs, please see the [Webex Meetings XML to REST Migration Guide](https://developer.cisco.com/docs/webex-meetings/#xml-to-rest-migration-guide). User management APIs such as `CreateUser`, `SetUser`, `DelUser`, etc. are **NOT** affected by this EOL announcement.

## Selected section

## Creating and Using Webex Apps

The base URL for the Webex REST API is <https://webexapis.com/v1/>. Detailed information about each API resource and endpoint can be found in the [API Reference](https://developer.webex.com/docs/api/v1/meetings).

The Meetings-related APIs can be used with Webex Integrations. If you aren't familiar with integrations, check out the [Integrations Guide](https://developer.webex.com/docs/integrations) for more information. To create a new integration, select [My Webex Apps](https://developer.webex.com/my-apps) from the menu under your avatar at the top of this page to get started.

To use the Webex REST API you'll need to be a Webex Meetings subscriber with a Webex account backed by Cisco Webex Common Identity (CI). If you currently use Webex, your account is backed by Common Identity. If you're using only Webex Meetings, your site will [need to be on Common Identity](https://help.webex.com/WBX000023841/).
