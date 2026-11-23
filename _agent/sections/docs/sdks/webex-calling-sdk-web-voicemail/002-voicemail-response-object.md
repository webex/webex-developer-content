---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-web-voicemail
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Voicemail Response Object
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-voicemail). [Full Markdown](../../../../../docs/sdks/webex-calling-sdk-web-voicemail.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The `VoicemailClient` object is a supplementary Calling SDK module that adds comprehensive support for voicemail functionality. 

---

Before continuing, refer to the [Quickstart Guide](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-quickstart) to understand how `Call` objects are created and how different modules are instantiated. The `VoicemailClient` object offers a variety of functions which are covered in this article in detail.

## Selected section

## Voicemail Response Object

Here's an example response from the voicemailClient method:

```javascript
{
  statusCode: number;
  data: {
    voicemailList?: MessageInfo[];
    voicemailContent?: {
      type: string | null;
      content: string | null;
    };
    voicemailSummary?: SummaryInfo;
    voicemailTranscript?: string | null;
    error?: string;
  };
  message: string | null;
};
```

### Fetch a Voicemail List

The `getVoicemailList()` method retrieves the voicemails present in the voicemail box of the user:

```javascript
const voicemailListResponse = await voicemailClient.getVoicemailList(
  OFFSET,
  OFFSETLIMIT,
  SORT.DESC,
  true
);
```

The following table describes the options available for the arguments passed to the `getVoicemailList()` method:



<table>
  <colgroup>
    <col style="width: 12%" />
    <col style="width: 88%" />
  </colgroup>
  <tbody>
    <tr>
      <td><strong>Parameters</strong></td>
      <td>
        <p>Options</p>
        
          <table>
            <tbody>
              <tr>
                <th colspan="1"><strong>Name</strong></th>
                <th colspan="1"><strong>Description</strong></th>
                <th colspan="1"><strong>Values</strong></th>
                <th colspan="1"><strong>Required</strong></th>
              </tr>
              <tr>
                <td><code>sort</code></td>
                <td>
                  Sorting order of voicemail list, ASC or DESC.
                </td>
                <td>
                  <p>
                    <em><strong>String</strong></em>
                  </p>
                  
                    <table>
                      <tbody>
                        <tr>
                          <td>
                            <strong>ASC</strong>
                          </td>
                          <td>
                            <strong>DESC</strong>
                          </td>
                        </tr>
                      </tbody>
                    </table>
                  
                </td>
                <td>yes</td>
              </tr>
              <tr>
                <td><code>offset</code></td>
                <td>
                  Number of records to skip.
                </td>
                <td>
                  <p>
                    <strong>Number</strong>
                </td>
                <td>yes</td>
              </tr>
              <tr>
                <td><code>offsetLimit</code></td>
                <td>
                  Index of the voicemail to fetch from the voicemail list.
                </td>
                <td>
                  <strong>String</strong>
                </td>
                <td>yes</td>
              </tr>
              <tr>
                <td colspan="1"><code>refresh</code></td>
                <td colspan="1">
                  Refresh the list of voicemails from the backend.
                </td>
                <td colspan="1">
                  <strong>Boolean</strong>
                </td>
                <td colspan="1">yes</td>
              </tr>
            </tbody>
          </table>
        
      </td>
    </tr>
  </tbody>
</table>



|            |                                   |
| ---------- | --------------------------------- |
| Parameters | See table above                   |
| Returns    | Promise\<VoicemailResponseEvent\> |
