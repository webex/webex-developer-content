---
type: Guide
title: Web Calling SDK | Supplementary Services
display_title: Supplementary Services
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-web-supplementary-services
content_type: documentation
product_group:
- webex-suite
categories:
- calling
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-supplementary-services)

This article describes the Webex Calling SDK supplementary services such as hold, resume, blind transfer, and consult transfer.

---

Once an inbound or outbound call is in an established state, you can access a set of supplementary services. To access these services, you'll need the `Call` object, which is created when a call is initialized. Refer to [Inbound/Outbound Calls](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-incoming-outgoing-calls) for information on creating a `Call` object.

The Call object exposes the following supplementary service methods:

- `doHoldResume()`
- `completeTransfer()`
- `sendDigit()`

## doHoldResume Method

The `doHoldResume()` method puts the call on hold or resumes based on the current state of the call. If the call is connected, it's put on hold. Likewise if the call is already on hold, `doHoldResume()` resumes the call.



|            |      |
| ---------- | ---- |
| Parameters | --   |
| Returns    | void |

```javascript
// Assuming the call(inbound/outbound) is already established and we have the call instance.

call.doHoldResume(); // call is put on hold

call.doHoldResume(); // call is resumed
```

You'll want to create a listener for the `held` event on the `Call` object to monitor the hold status of the call:

```javascript
call.on('held', (callId: CallId) => {
  // Add code to handle successful hold
});
```

If the hold action is not successful, the `Call` object emits a `hold_error` event:

```javascript
call.on('hold_error', (error: CallError) => {
  // Add code to handle hold error
});
```

If a call is resumed from hold successfully, the `Call` object emits a `resumed` event:

```javascript
call.on('resumed', (callId: CallId) => {
  // Add code to handle successful resume
});
```

if the call is not resumed successfully, the `Call` object emits a `resume_error`:

```javascript
call.on('resume_error', (error: CallError) => {
  // Add code to handle resume error
});
```

## completeTransfer Method

The completeTransfer() method initiate call transfers. The Calling SDK supports two types of transfers: blind transfer and a consult transfer.

The method accepts three arguments:

- `transferType`
- `transferCallID`
- `transferTarget`

The following table provides more details:



<table>
  <colgroup>
    <col />
    <col />
  </colgroup>
  <tbody>
    <tr>
      <td><strong>Parameters</strong></td>
      <td>
        
          <table>
            <tbody>
              <tr>
                <th colspan="1"><strong>Name</strong></th>
                <th colspan="1"><strong>Description</strong></th>
                <th colspan="1"><strong>Values</strong></th>
                <th colspan="1"><strong>Required</strong></th>
              </tr>
              <tr>
                <td><code>transferType</code></td>
                <td>
                  Controls which type of transfer is triggered.
                </td>
                <td>
                  <p>
                    
                      <strong>enum TransferType</strong>
                    
                  </p>
                  
                    <table>
                      <tbody>
                        <tr>
                          <th><strong>BLIND</strong></th>
                          <th><strong>CONSULT</strong></th>
                        </tr>
                      </tbody>
                    </table>
                  
                </td>
                <td>Yes</td>
              </tr>
              <tr>
                <td><code>transferCallId</code></td>
                <td>
                  Call ID where the current call will be merged for consult transfers.
                </td>
                <td>
                    <strong>
                      string
                    </strong>
                </td>
                <td>No</td>
              </tr>
              <tr>
                <td><code>transferTarget</code></td>
                <td>Destination for blind transfer.</td>
                <td>
                  <strong>string</strong>
                </td>
                <td>No</td>
              </tr>
            </tbody>
          </table>
        
      </td>
    </tr>
    <tr>
      <td colspan="1">
        <strong>Returns</strong>
      </td>
      <td colspan="1">
        <strong>void</strong></p>
      </td>
    </tr>
  </tbody>
</table>

### Blind Transfer

A blind transfer involves transferring a call to a destination without first consulting with the person to whom the call is being transferred. To initiate a blind transfer, set the `transferType` to `BLIND` and provide the `transferTarget`. For a blind transfer, `transferTarget` is mandatory. A `transferCallId` is not required for a blind transfer.

```javascript
const call = line.makeCall();
const destination = '123456789';
// Note: transferCallId is used for consult transfer, and must be undefined for a blind transfer.
call.completeTransfer(TransferType.BLIND, undefined, destination); 
```

### Consult Transfer

A consult transfer involves consulting with a new user before transferring the call to them. To initiate a consult transfer, set the `transferType` to `CONSULT` and provide the `transferCallId`. For a consult transfer, `transferCallId` is a mandatory argument. `transferTarget` is not required for a consult transfer.

Here's the workflow for a typical consult transfer:

1. **UserA** calls **UserB**. At this point, either of the users can transfer the call.
1. **UserB** wants to transfer the call. **UserB** will first have to put **UserA** on hold.
1. Now **UserB** will be able to dial out to UserC.
1. Once UserC answers, **UserB** and **UserC** will be in a connected call while **UserA** is on hold.
1. The `completeTransfer()` method can be invoked to allow **UserB** to transfer the call.
1. The `CallId` between **UserA** and **UserB** is the `transferCallId` and is passed to the method.
1. If the transfer is successful, **UserA** and **UserC** will be on a call and **UserB** will get disconnected from both the calls.

```javascript
// callAB -> call between UserA and UserB
// callBC -> call between UserB and UserC

// UserA calls UserB
const callAB = line.makeCall();

// UserB puts UserA on hold
callAB.doHoldResume();

// UserB calls UserC
const callBC = line.makeCall();

// UserB completes the transfer
callAB.completeTransfer(TransferType.CONSULT, CallBC.getCallId());
```

If transfer is not successful, the `CAll` object emits a 'transfer_error' event. 

```javascript
call.on('transfer_error', (error: CallError) => {
  // Add code to handle transfer error
});
```

The `CallError` object contains the following members:



|**Properties**|**Description**|**Type**|
| --- | --- | --- |
|`message`| Description of error in the `callingClient`|  `ErrorMessage` |
|`context`|  Error Context as generated by the caller. | `ErrorContext` |
|`type`|  Type of error in the `callingClient`| `ERROR_TYPE`|
|`correlationId`| Correlation ID of the call that faced the issue.| `string` |
|`errorLayer`| Layer at which error occurred, either `media` or `call_control`.|`ERROR_LAYER`|

## sendDigit Method

The `sendDigit()` method sends a single DTMF digit on an established call which is useful, for instance, when navigating an Interactive Voice Response (IVR) system where a user is expected to enter a touch tone corresponding to menu item.

The method accepts a string representing the DTMF digit as a parameter:



|            |        |
| ---------- | ------ |
| Parameters | `string` |
| Returns    | `void`   |

```javascript
const call = line.makeCall();
call.sendDigit('1');
```
