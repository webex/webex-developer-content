---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-advanced-meeting-controls
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Cancel Calling Out a SIP Participant
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-advanced-meeting-controls). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-web-advanced-meeting-controls.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article describes the advanced meeting controls available in the Webex Web SDK for meetings.

## Selected section

## Cancel Calling Out a SIP Participant

To cancel an ongoing SIP call-out, use the `Meeting` object's `cancelSipCallOut()` method and pass the ID of the participant whose call-out you wish to cancel.

```javascript
await meeting.cancelSipCallOut(participantId);
```



<table>
  <colgroup>
    <col/>
    <col/>
  </colgroup>
  <tbody>
    <tr>
      <td><strong>Asynchronous</strong></td>
      <td>Yes</td>
    </tr>
    <tr>
      <td><strong>Parameters</strong></td>
      <td>
        
          <table>
            <tbody>
              <tr>
                <th><strong>Sl. No</strong></th>
                <th colspan="1"><strong>Parameter Name</strong></th>
                <th><strong>Parameter Type</strong></th>
                <th><strong>Mandatory</strong></th>
                <th><strong>Description</strong></th>
              </tr>
              <tr>
                <td>1</td>
                <td><code>participantId</code></td>
                <td><strong>String</strong></td>
                <td>Yes</td>
                <td><p>The ID of the participant returned by the `sipCallOut` method whose SIP call-out should be cancelled.</p>
                </td>
              </tr>
            </tbody>
          </table>
        
      </td>
    </tr>
    <tr>
      <td><strong>Returns</strong></td>
      <td><code>Promise&lt;undefined&gt;</code></td>
    </tr>
  </tbody>
</table>
