---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-calling-move-user-api-workflows
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Getting Started
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-calling-move-user-api-workflows). [Full Markdown](../../../../docs/webex-calling-move-user-api-workflows.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The [Webex Calling platform](https://developer.webex.com/docs/webex-calling-overview) provides comprehensive APIs for managing user configurations and locations. Among the most critical administrative operations is the ability to move users between locations while preserving their calling settings and minimizing service disruption. The Move User APIs enable administrators to automate complex user relocation scenarios that would otherwise require extensive manual configuration in [Webex Control Hub](https://www.webex.com/control-hub.html).

---

User moves in Webex Calling involve transferring users from one location to another within the same organization, along with their associated phone numbers and/or extensions, or assigning new ones as needed. For further details on features that are retained/removed during a move, see the `Features` section in [Move Calling users](https://help.webex.com/en-us/article/h68cdcb/Move-users-from-one-location-to-another#wbxch_t_move_user) help document.

## Selected section

## Getting Started

The Move User APIs require full administrator privileges and specific scopes for execution. Begin by ensuring you have the proper authentication and permissions, then follow a validation-first approach to minimize disruption during user moves.

### Prerequisites

- **Full administrator auth token** with scopes: `spark-admin:telephony_config_write`, `spark-admin:people_write`, and `identity:groups_rw`
- **Read-only administrator auth token** (for monitoring operations) with scope: `spark-admin:telephony_config_read`
- **Webex Calling enabled organization** with multiple locations configured

### Recommended Workflow

1. **Plan the move** by identifying source and target locations, users to be moved, and desired phone numbers/extensions
2. **Validate first** if it is for a single calling user using `validate: true` to identify all potential errors and impacts (see [Validation Workflow](https://developer.webex.com/docs/webex-calling-move-user-api-workflows#validation-workflow))
3. **Resolve errors** identified from the validation workflow
4. **Execute the move** using `validate: false` after validation is clean (for a single calling user) or directly for bulk operations
5. **Monitor progress** using the [job status APIs](https://developer.webex.com/docs/webex-calling-move-user-api-workflows#job-monitoring-and-status-workflow) for asynchronous move operations
6. **Handle errors** by reviewing [detailed error reports](https://developer.webex.com/docs/webex-calling-move-user-api-workflows#common-error-codes-and-responses) and retrying failed moves after resolution


<a id="common-error-codes-and-responses"></a>
