---
type: Guide
title: Webex Status API
display_title: Webex Status API
canonical_url: https://developer.webex.com/docs/webex-status-api
content_type: documentation
product_group:
- webex-suite
categories:
- calling
- meeting
- messaging
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/webex-status-api)

The Webex status API lets you programmatically access comprehensive data on the status of Webex services.

---



> **Info**
>
> This documentation is external to the Webex Developer Portal.



 - [Status summary][1] &mdash; Get a summary of the status page, including a status indicator, component statuses, unresolved incidents, and any upcoming or in-progress scheduled maintenances.
 - [Complete status rollup][2] &mdash; Get the components for the status page. Each component is listed along with its status - one of operational, under_maintenance,degraded_performance, partial_outage, or major_outage.
 - [Status page components][3] &mdash; Get the components for the status page. Each component is listed along with its status - one of operational, under_maintenance,degraded_performance, partial_outage, or major_outage.
 - [Unresolved incidents][4] &mdash; Get a list of any unresolved incidents. This response will only return incidents in the Investigating, Identified, or Monitoring state.
 - [50 most recent incidents][5] &mdash; Includes all unresolved incidents as described above, as well as those in the Resolved state.
 - [Upcoming scheduled maintenance][6] &mdash; Get a list of any upcoming maintenances. This response will only return scheduled maintenances still in the Scheduled state.
 - [Active scheduled maintenance][7] &mdash; Get a list of any active maintenances. This response will only return scheduled maintenances in the In Progress state.
 - [50 most recent scheduled maintenances][8] &mdash; Includes scheduled maintenances in Scheduled , In Progress or Completed state.


  [1]: https://status.webex.com/api/#Summary
  [2]: https://status.webex.com/api/#Status
  [3]: https://status.webex.com/api/#Components
  [4]: https://status.webex.com/api/#Unresolved-incidents
  [5]: https://status.webex.com/api/#All-incidents
  [6]: https://status.webex.com/api/#Upcoming-scheduled-maintenances
  [7]: https://status.webex.com/api/#Active-scheduled-maintenances
  [8]: https://status.webex.com/api/#All-scheduled-maintenances
