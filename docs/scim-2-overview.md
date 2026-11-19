---
type: Guide
title: SCIM-2 Overview
display_title: SCIM-2 Overview
canonical_url: https://developer.webex.com/docs/scim-2-overview
content_type: documentation
product_group:
- webex-suite
categories:
- admin
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/scim-2-overview)

System for Cross Domain Identity Management (SCIM) 

---

The System for Cross Domain Identity Management (SCIM) is an Internet Task Engineering Force (IETF) standard for transmitting digital identity data between domains. The SCIM 2.0 standard is published with the IETF at [SCIM Protocol](https://www.rfc-editor.org/rfc/rfc7644) and [SCIM Schema](https://www.rfc-editor.org/rfc/rfc7644). Webex supports both the Core Schema and Enterprise Extension schema. This standard allows for interoperability with SCIM 2.0 compliant clients and simplifies automating user identity provisioning to Webex.

## SCIM Endpoints and HTTP Methods

The SCIM protocol defines HTTP methods and endpoints for managing resources, such as "User" and "Group" resources that correspond to "/Users" and "/Groups".



| **HTTP method** | **SCIM Usage**  |
|-------------|-------------|
| GET    | Retrieves one or more complete or partial resources.                                                                                                            |
| POST   | Depending on the endpoint, creates new resources, or may be used to bulk-modify resources.                                                                      |
| PUT    | Modifies a resource by replacing existing attributes with a specified set of replacement attributes (replace).  PUT should not be used to create new resources. |
| PATCH  | Modifies a resource with a set of client-specified changes. (partial update).                                                                                   |
| DELETE | Deletes a resource.                                                                                                                                             |

## Supported attributes and Schemas



| **Schema**                                                 | **Supported attributes**         |
|--------|-----|
| urn:ietf:params:scim:schemas:core:2.0:User                 | id (readonly)<br/>userName<br/>active<br/>roles<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;value<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;type<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;display<br/>name<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;givenName<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;familyName<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;middleName<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;honorificPrefix<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;honorificSuffix<br/>displayName<br/>nickName<br/>emails<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;value<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;type<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;display<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;primary<br/>userType<br/>profileUrl<br/>title<br/>preferredLanguage<br/>locale<br/>externalId<br/>timezone<br/>phoneNumbers<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;value<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;type<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;display<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;primary<br/>photos<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;value<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;type<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;display<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;primary<br/>addresses<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;type<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;streetAddress<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;locality<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;region<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;postalCode<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;country |
| urn:ietf:params:scim:schemas:extension:enterprise:2.0:User | costCenter<br/>organization<br/>division<br/>department<br/>employeeNumber<br/>manager<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;value<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;displayName<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$ref (readonly)      |
| urn:scim:schemas:extension:cisco:webexidentity:2.0:User    | accountStatus<br/>sipAddresses<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;value<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;type<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;display<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;primary<br/>managedOrgs<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;orgId<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;role<br/>managedGroups (readonly)<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;orgId<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;groupId<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;role<br/>extensionAttribute(1-15)<br/> externalAttribute(1-15)<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;source<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;value      |
