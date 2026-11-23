---
type: Excerpt
canonical_url: https://developer.webex.com/docs/scim-2-overview
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Supported attributes and Schemas
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/scim-2-overview). [Full Markdown](../../../../docs/scim-2-overview.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

System for Cross Domain Identity Management (SCIM) 

---

The System for Cross Domain Identity Management (SCIM) is an Internet Task Engineering Force (IETF) standard for transmitting digital identity data between domains. The SCIM 2.0 standard is published with the IETF at [SCIM Protocol](https://www.rfc-editor.org/rfc/rfc7644) and [SCIM Schema](https://www.rfc-editor.org/rfc/rfc7644). Webex supports both the Core Schema and Enterprise Extension schema. This standard allows for interoperability with SCIM 2.0 compliant clients and simplifies automating user identity provisioning to Webex.

## Selected section

## Supported attributes and Schemas



| **Schema**                                                 | **Supported attributes**         |
|--------|-----|
| urn:ietf:params:scim:schemas:core:2.0:User                 | id (readonly)<br/>userName<br/>active<br/>roles<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;value<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;type<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;display<br/>name<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;givenName<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;familyName<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;middleName<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;honorificPrefix<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;honorificSuffix<br/>displayName<br/>nickName<br/>emails<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;value<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;type<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;display<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;primary<br/>userType<br/>profileUrl<br/>title<br/>preferredLanguage<br/>locale<br/>externalId<br/>timezone<br/>phoneNumbers<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;value<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;type<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;display<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;primary<br/>photos<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;value<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;type<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;display<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;primary<br/>addresses<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;type<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;streetAddress<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;locality<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;region<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;postalCode<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;country |
| urn:ietf:params:scim:schemas:extension:enterprise:2.0:User | costCenter<br/>organization<br/>division<br/>department<br/>employeeNumber<br/>manager<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;value<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;displayName<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$ref (readonly)      |
| urn:scim:schemas:extension:cisco:webexidentity:2.0:User    | accountStatus<br/>sipAddresses<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;value<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;type<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;display<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;primary<br/>managedOrgs<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;orgId<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;role<br/>managedGroups (readonly)<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;orgId<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;groupId<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;role<br/>extensionAttribute(1-15)<br/> externalAttribute(1-15)<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;source<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;value      |
