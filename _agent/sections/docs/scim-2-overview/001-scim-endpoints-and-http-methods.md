---
type: Excerpt
canonical_url: https://developer.webex.com/docs/scim-2-overview
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- SCIM Endpoints and HTTP Methods
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/scim-2-overview). [Full Markdown](../../../../docs/scim-2-overview.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

System for Cross Domain Identity Management (SCIM) 

---

The System for Cross Domain Identity Management (SCIM) is an Internet Task Engineering Force (IETF) standard for transmitting digital identity data between domains. The SCIM 2.0 standard is published with the IETF at [SCIM Protocol](https://www.rfc-editor.org/rfc/rfc7644) and [SCIM Schema](https://www.rfc-editor.org/rfc/rfc7644). Webex supports both the Core Schema and Enterprise Extension schema. This standard allows for interoperability with SCIM 2.0 compliant clients and simplifies automating user identity provisioning to Webex.

## Selected section

## SCIM Endpoints and HTTP Methods

The SCIM protocol defines HTTP methods and endpoints for managing resources, such as "User" and "Group" resources that correspond to "/Users" and "/Groups".



| **HTTP method** | **SCIM Usage**  |
|-------------|-------------|
| GET    | Retrieves one or more complete or partial resources.                                                                                                            |
| POST   | Depending on the endpoint, creates new resources, or may be used to bulk-modify resources.                                                                      |
| PUT    | Modifies a resource by replacing existing attributes with a specified set of replacement attributes (replace).  PUT should not be used to create new resources. |
| PATCH  | Modifies a resource with a set of client-specified changes. (partial update).                                                                                   |
| DELETE | Deletes a resource.                                                                                                                                             |
