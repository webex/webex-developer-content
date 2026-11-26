---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-calling-move-user-api-workflows
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Common Error Codes and Responses
- HTTP Status Codes
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-calling-move-user-api-workflows). [Full Markdown](../../../../docs/webex-calling-move-user-api-workflows.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Getting Started](002-getting-started.md)

## Article introduction

The [Webex Calling platform](https://developer.webex.com/docs/webex-calling-overview) provides comprehensive APIs for managing user configurations and locations. Among the most critical administrative operations is the ability to move users between locations while preserving their calling settings and minimizing service disruption. The Move User APIs enable administrators to automate complex user relocation scenarios that would otherwise require extensive manual configuration in [Webex Control Hub](https://www.webex.com/control-hub.html).

---

User moves in Webex Calling involve transferring users from one location to another within the same organization, along with their associated phone numbers and/or extensions, or assigning new ones as needed. For further details on features that are retained/removed during a move, see the `Features` section in [Move Calling users](https://help.webex.com/en-us/article/h68cdcb/Move-users-from-one-location-to-another#wbxch_t_move_user) help document.

## Parent context

## Common Error Codes and Responses

The Move User APIs return specific error codes to help identify and resolve issues during validation and execution. Understanding these error codes is essential for proper error handling and troubleshooting.

## Selected section

### HTTP Status Codes

| Status Code | Description | Common Causes |
|-------------|-------------|---------------|
| `200` | Success | Request processed successfully (for validation and status checks) |
| `201` | Created | Initial validations passed successfully and job has been created to move the users |
| `400` | Bad Request | Invalid request format, missing required fields, validation errors |
| `500` | Internal Server Error | Server-side processing errors, gateway issues |
