---
type: Excerpt
canonical_url: https://developer.webex.com/docs/meetings
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Meeting Template Locales
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

## Meeting Template Locales

Meetings can be created by meeting templates. The list of meeting templates that is available for the authenticated user can be retrieved from [List Meeting Templates](https://developer.webex.com/docs/api/v1/meetings/list-meeting-templates) API with different values of `locale`. All the locales supported by Webex are listed below:



| Language | Country/Region | Locale Name | Default Locale |
|---|---|---|---|
| Bulgarian | Bulgaria | bg_BG |  |
| Castilian Spanish | Spain | es_SP |  |
| Chinese (Simplified) | China | zh_CN |  |
| Chinese (Traditional) | Taiwan | zh_TW |  |
| Croatian | Croatia | hr_HR |  |
| Czech | Czech Republic | cs_CZ |  |
| Danish | Denmark | da_DK |  |
| Dutch | Netherlands | nl_NL |  |
| English | United Kingdom | en_GB |  |
| English | United States | en_US | Yes |
| French | Canada | fr_CA |  |
| French | France | fr_FR |  |
| German | Germany | de_DE |  |
| Hungarian | Hungary | hu_HU |  |
| Italian | Italy | it_IT |  |
| Japanese | Japan | ja_JP |  |
| Korean | Korea | ko_KR |  |
| Norwegian | Norway | no_NO |  |
| Polish | Poland | pl_PL |  |
| Portuguese | Brazil | pt_BR |  |
| Romanian | Romania | ro_RO |  |
| Russian | Russia | ru_RU |  |
| Serbian | Serbia | sr_RS |  |
| Spanish | Mexico | es_ES |  |
| Swedish | Sweden | sv_SE |  |
| Turkish | Turkey | tr_TR |  |
