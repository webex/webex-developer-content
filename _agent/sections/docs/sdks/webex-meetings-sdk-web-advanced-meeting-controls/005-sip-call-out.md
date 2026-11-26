---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-advanced-meeting-controls
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- SIP Call Out
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-advanced-meeting-controls). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-web-advanced-meeting-controls.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article describes the advanced meeting controls available in the Webex Web SDK for meetings.

## Selected section

## SIP Call Out

To call out a SIP participant to a meeting, use the `Meeting` object's `sipCallOut()` method and pass the SIP address and display name of the participant you want to call.

```javascript
await meeting.sipCallOut(address, displayName);
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
                <td><code>address</code></td>
                <td><strong>String</strong></td>
                <td>Yes</td>
                <td><p>The SIP address of the invited SIP participant.</p></td>
              </tr>
              <tr>
                <td>2</td>
                <td><code>DisplayName</code></td>
                <td><strong>String</strong></td>
                <td>Yes</td>
                <td><p>The display name of the invited SIP participant.</p></td>
              </tr>
            </tbody>
          </table>
        
      </td>
    </tr>
    <tr>
      <td><strong>Returns</strong></td>
      <td><code>Promise&lt;Object&gt;</code> - Returns an object containing participant details:
        <pre>
          <code>
            {
              "participantId":"abc123-def456-ghi789",
              "address": "sip:user@example.com",
              "displayName": "John Doe",
              "status": "pending"
            }
          </code>
        </pre>
      </td>
    </tr>
  </tbody>
</table>



> **Info**
>
> NOTE: The participant list is not automatically updated when a SIP call-out is initiated. You must save the `participantId` returned by this method to use with `cancelSipCallOut()` if you need to cancel the call-out later. To track when a SIP participant actually joins the meeting after the call-out, listen to the `members:update` event, which provides details about new participants joining the meeting.
