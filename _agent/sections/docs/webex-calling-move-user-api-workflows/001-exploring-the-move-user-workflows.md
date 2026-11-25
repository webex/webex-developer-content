---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-calling-move-user-api-workflows
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Exploring the Move User Workflows
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-calling-move-user-api-workflows). [Full Markdown](../../../../docs/webex-calling-move-user-api-workflows.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Getting Started](002-getting-started.md)

## Article introduction

The [Webex Calling platform](https://developer.webex.com/docs/webex-calling-overview) provides comprehensive APIs for managing user configurations and locations. Among the most critical administrative operations is the ability to move users between locations while preserving their calling settings and minimizing service disruption. The Move User APIs enable administrators to automate complex user relocation scenarios that would otherwise require extensive manual configuration in [Webex Control Hub](https://www.webex.com/control-hub.html).

---

User moves in Webex Calling involve transferring users from one location to another within the same organization, along with their associated phone numbers and/or extensions, or assigning new ones as needed. For further details on features that are retained/removed during a move, see the `Features` section in [Move Calling users](https://help.webex.com/en-us/article/h68cdcb/Move-users-from-one-location-to-another#wbxch_t_move_user) help document.

## Selected section

## Exploring the Move User Workflows

The Move User APIs support both single-user and bulk operations, with the ability to move up to 100 users in a single request. These APIs provide several distinct workflows designed to handle different aspects of the user relocation process. The workflows can be grouped into validation, execution, and monitoring categories, each serving specific operational needs:

<a id="validation-workflow"></a>

### Validation Workflow

**[Validate Move Users Job](https://developer.webex.com/docs/api/v1/user-call-settings-2-2/validate-or-initiate-move-users-job)** with [`validate: true`](https://developer.webex.com/docs/webex-calling-move-user-api-workflows#single-user-validation-request) allows administrators to preview the impact of moving users before executing the actual move operation. This enables administrators to perform a complete set of validations, returning the results synchronously. The [initial request validations](https://developer.webex.com/docs/webex-calling-move-user-api-workflows#initial-request-validation-errors) are performed first, and if no errors are found at this stage, the system proceeds with [comprehensive request validations](https://developer.webex.com/docs/webex-calling-move-user-api-workflows#comprehensive-request-validation-errors) and returns detailed `impacts` and `errors` arrays that help administrators understand the potential impacts of proceeding with the move, as well as any hard stops that may prevent the move.

Note: The validation workflow is supported only for single calling user moves.

### Move Execution Workflow

**[Execute Move Users Job](https://developer.webex.com/docs/api/v1/user-call-settings-2-2/validate-or-initiate-move-users-job)** with [`validate: false`](https://developer.webex.com/docs/webex-calling-move-user-api-workflows#single-user-move-request) performs the actual user relocation. This workflow supports both calling and non-calling user moves. [Initial request validations](https://developer.webex.com/docs/webex-calling-move-user-api-workflows#initial-request-validation-errors) are performed first, and only if these pass does the system proceed with the actual user move. 

For a single non-calling user, no job is created and the move executes synchronously. 

On the other hand, for a single calling user or bulk user moves, a job is created. A job is created for asynchronous operations, showing up in Control Hub as a task. Each job may execute multiple steps that can be monitored for progress and completion status, predominantly used for bulk processing of records. During move user job execution, additional [comprehensive request validation errors](https://developer.webex.com/docs/webex-calling-move-user-api-workflows#comprehensive-request-validation-errors) may occur, which can be viewed via the [List Move Users Job Errors](https://developer.webex.com/docs/api/v1/user-call-settings-2-2/list-move-users-job-errors) API or CSV downloads from the [Get Move Users Job Status](https://developer.webex.com/docs/api/v1/user-call-settings-2-2/get-move-users-job-status) API.


<a id="job-monitoring-and-status-workflow"></a>

### Job Monitoring and Status Workflow

For all jobs, corresponding monitoring APIs are defined that provide real-time visibility into job progress, completion status, and detailed error reporting. For the move user jobs, it consists of the below APIs:

- **[List Move Users Jobs](https://developer.webex.com/docs/api/v1/user-call-settings-2-2/list-move-users-jobs)** retrieves all move jobs for an organization, ordered by most recent first, with status information and completion counts.
- **[Get Move Users Job Status](https://developer.webex.com/docs/api/v1/user-call-settings-2-2/get-move-users-job-status)** provides detailed status information for a specific job, including execution timestamps, step-by-step progress, and CSV download links for detailed results.
- **[List Move Users Job Errors](https://developer.webex.com/docs/api/v1/user-call-settings-2-2/list-move-users-job-errors)** returns detailed error information for a specific job that completed with errors, helping administrators identify and resolve specific user move failures.

The monitoring capabilities include:
- **Real-time status tracking** with job execution states (STARTED, COMPLETED, COMPLETED_WITH_ERRORS, FAILED)
- **Progress counters** showing total moves, successful moves, failed moves, and pending moves
- **Detailed error reporting** with specific error codes and messages for troubleshooting
- **CSV export functionality** for comprehensive move results and audit trails
