---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-calling-move-user-api-workflows
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Common Error Codes and Responses
- Validation Error Codes
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

### Validation Error Codes

The Move User APIs use different categories of validation error codes depending on when validation occurs in the request lifecycle. Understanding these categories helps with proper error handling and troubleshooting.

#### Hard Stop Validation Errors

Typically, all validation failures for a user move request will be consolidated and returned together. This means that if a user has multiple validation issues, all errors will be collected and returned together, allowing administrators to address all problems in one iteration.

However, there are certain exceptions where validation consolidation does not apply and the request is rejected immediately. Some of these cases include:
- **Request has more users than the allowed limit**
- **Request JSON syntax errors** - Malformed JSON prevents further processing
- **JSON parse errors** - Invalid JSON structure stops validation
- **Malformed Webex resource type** - Fundamental format issues
- **Duplicate users and empty users** - Their related fields (locationId/extension/phoneNumber) are not validated, but other unique users in the request are still validated

<a id="initial-request-validation-errors"></a>

#### Initial Request Validation Errors

For all requests, regardless of the `validate` attribute value, a basic set of validations is performed synchronously. These validations include basic request format checks, user ID validation, and business rule verification. Any validation failures at this stage are returned synchronously in the `errors` array field of the [error response](https://developer.webex.com/docs/webex-calling-move-user-api-workflows#error-response) with the appropriate error codes and status code `400`.

The possible error codes that can occur during initial API request validation include:

| Error Code | Message |
|------------|---------|
| `400` | Users should not be empty. |
| `1026006` | Attribute 'User ID' is required. |
| `1026006` | Attribute 'Validate' is required. |
| `1026011` | Users list should not be empty. |
| `1026013` | The source and the target location cannot be the same. |
| `1026014` | Error occurred while processing the move users request. |
| `1026016` | User should have either phone number or extension. |
| `1001804` | The extension specified is not valid. |
| `1026017` | Phone number is not in e164 format. |
| `1026018` | Selected Users list exceeds the maximum limit. |
| `1026019` | Duplicate entry for user is not allowed. |
| `1026020` | Validate 'true' is supported only for single user. |
| `1026021` | Attribute location id is required for Calling user. |
| `1026022` | Validate 'true' is supported for calling users only. |
| `1026024` | Invalid Location Id. |
| `1026024` | Invalid User Id. |
| `2150012` | User was not found |
| `1026015` | Error occurred while moving user number to target location.(Applicable to single calling user move, validate=true) |
| `1026023` | Extension and phone number is supported for calling users only.(Applicable to single non-calling user move, validate=false) |

<a id="comprehensive-request-validation-errors"></a>

#### Comprehensive Request Validation Errors

These error codes can occur during comprehensive validation of user moves. 

When the `validate` attribute is set to `true` for a single calling user, these errors are returned synchronously in the `errors` array field of the [validation response](https://developer.webex.com/docs/webex-calling-move-user-api-workflows#validation-response) with the status code `200`. 

When the `validate` attribute is set to `false`, these errors are validated during job execution and can be found via the [List Move Users Job Errors](https://developer.webex.com/docs/api/v1/user-call-settings-2-2/list-move-users-job-errors) API in the `items[].error` field, and the CSV download from the [Get Move Users Job Status](https://developer.webex.com/docs/api/v1/user-call-settings-2-2/get-move-users-job-status) API. 

The possible validation errors are:

| Error Code | Message |
|------------|---------|
| `4003` | User Not Found |
| `4007` | User Not Found |
| `4152` | Location Not Found |
| `5620` | Location Not Found |
| `4202` | The extension is not available. It is already assigned to a user : {0} |
| `8264` | Routing profile is different with new group: {0} |
| `19600` | User has to be within an enterprise to be moved. |
| `19601` | User can only be moved to a different group within the same enterprise. |
| `19602` | Only regular end user can be moved. Service instance virtual user cannot be moved. |
| `19603` | New group already reaches maximum number of user limits. |
| `19604` | The {0} number of the user is the same as the calling line ID of the group. |
| `19605` | User is assigned services not authorized to the new group: {0}. |
| `19606` | User is in an active hoteling/flexible seating association. |
| `19607` | User is pilot user of a trunk group. |
| `19608` | User is using group level device profiles which is used by other users in current group. Following are the device profiles shared with other users: {0}. |
| `19609` | Following device profiles cannot be moved to the new group because there are already devices with the same name defined in the new group: {0}. |
| `19610` | The extension of the user is used as transfer to operator number for following Auto Attendent : {0}. |
| `19611` | Fail to move announcement file from {0} to {1}. |
| `19612` | Fail to move device management file from {0} to {1}. |
| `19613` | User is assigned service packs not authorized to the new group: {0}. |
| `25008` | Missing Mandatory field name: {0} |
| `25110` | {fieldName} cannot be less than {0} or greater than {1} characters. |
| `25378` | Target location is same as user's current location. |
| `25379` | Error Occurred while Fetching User's Current Location Id. |
| `25381` | Error Occurred while rolling back to Old Location Call recording Settings |
| `25382` | Error Occurred while Disabling Call Recording for user which is required Before User can be Moved |
| `25383` | OCI Error while moving user |
| `25384` | Error Occurred while checking for Possible Call Recording Impact. |
| `25385` | Error Occurred while getting Call Recording Settings |
| `27559` | The groupExternalId search criteria contains groups with different calling zone. |
| `27960` | Parameter isWebexCalling, newPhoneNumber, or newExtension can only be set in Webex Calling deployment mode. |
| `27961` | Parameter isWebexCalling shall be set if newPhoneNumber or newExtension is set. |
| `27962` | Work space cannot be moved. |
| `27963` | Virtual profile user cannot be moved. |
| `27965` | The user's phone number: {0}, is same as the current group charge number. |
| `27966` | The phone number, {0}, is not available in the new group. |
| `27967` | User is configured as the ECBN user for another user in the current group. |
| `27968` | User is configured as the ECBN user for the current group. |
| `27969` | User is associated with DECT handset(s): {0} |
| `27970` | User is using a customer managed device: {0} |
| `27971` | User is using an ATA device: {0} |
| `27972` | User is in an active hotdesking association. |
| `27975` | Need to unassign CLID number from group before moving the number to the new group. Phone number: {0} |
| `27976` | Local Gateway configuration is different with new group. Phone number: {0} |
| `1026015` | Error occurred while moving user number to target location |
| `10010000` | Total numbers exceeded maximum limit allowed |
| `10010001` | to-location and from-location cannot be same |
| `10010002` | to-location and from-location should belong to same customer |
| `10010003` | to-location must have a carrier |
| `10010004` | from-location must have a carrier |
| `10010005` | Different Carrier move is not supported for non-Cisco PSTN carriers. |
| `10010006` | Number move not supported for WEBEX_DIRECT carriers. |
| `10010007` | Numbers out of sync, missing on CPAPI |
| `10010008` | from-location not found or pstn connection missing in CPAPI |
| `10010010` | from-location is in transition |
| `10010009` | to-location not found or pstn connection missing in CPAPI |
| `10010011` | to-location is in transition |
| `10010012` | Numbers don't have a carrier Id |
| `10010013` | Location less numbers don't have a carrier Id |
| `10010014` | Different Carrier move is not supported for numbers with different country or region. |
| `10010015` | Numbers contain mobile and non-mobile types. |
| `10010016` | To/From location carriers must be same for mobile numbers. |
| `10010017` | Move request for location less number not supported |
| `10010200` | Move request for more than one block number is not supported |
| `10010201` | Cannot move block number as few numbers not from the block starting %s to %s |
| `10010202` | Cannot move block number as few numbers failed VERIFICATION from the block %s to %s |
| `10010203` | Cannot move block number as few numbers missing from the block %s to %s |
| `10010204` | Cannot move number as it is NOT a part of the block %s to %s |
| `10010205` | Move request for Cisco PSTN block order not supported. |
| `10010299` | Move order couldn't be created as no valid number to move |
| `10030000` | Number not found |
| `10030001` | Number does not belong to from-location |
| `10030002` | Number is not present in CPAPI |
| `10030003` | Number assigned to an user or device |
| `10030004` | Number not in Active status |
| `10030005` | Number is set as main number of the location |
| `10030006` | Number has pending order associated with it |
| `10030007` | Number belongs to a location but a from-location was not set |
| `10030008` | Numbers from multiple carrier ids are not supported |
| `10030009` | Location less number belongs to a location. from-location value is set to null or no location id |
| `10030010` | One or more numbers are not portable. |
| `10030011` | Mobile number carrier was not set |
| `10030012` | Number must be assigned for assigned move |
| `10050000` | Failed to update customer reference for phone numbers on carrier |
| `10050001` | Failed to update customer reference |
| `10050002` | Order is not of operation type MOVE |
| `10050003` | CPAPI delete call failed |
| `10050004` | Not found in database |
| `10050005` | Error sending notification to WxcBillingService |
| `10050006` | CPAPI provision number as active call failed with status %s ,reason %s |
| `10050007` | Failed to update E911 Service |
| `10050008` | Target location does not have Inbound Toll Free license |
| `10050009` | Source location or Target location subscription found cancelled or suspended |
| `10050010` | Moving On Premises or Non Integrated CCP numbers from one location to another is not supported. |
| `10099999` | {Error Code} - {Error Message} |

#### Impact Codes

These impact codes indicate changes that will occur during the user move. 

When the `validate` attribute is set to `true` for a single calling user, these impacts are returned synchronously in the `impacts` array field of the [validation response](https://developer.webex.com/docs/webex-calling-move-user-api-workflows#validation-response) with the status code `200`. 

When the `validate` attribute is set to `false`, these impacts are available during job execution and can be found in the CSV download from the [Get Move Users Job Status](https://developer.webex.com/docs/api/v1/user-call-settings-2-2/get-move-users-job-status) API. 

The possible impacts are:

| Impact Code | Message |
|-------------|---------|
| `19701` | The identity/device profile the user is using is moved to the new group: {0}. |
| `19702` | The user level customized incoming digit string setting is removed from the user. User is set to use the new group setting. |
| `19703` | The user level customized outgoing digit plan setting is removed from the user. User is set to use the new group setting. |
| `19704` | The user level customized enhanced outgoing calling plan setting is removed from the user. User is set to use the new group setting. |
| `19705` | User is removed from following group services: {0}. |
| `19706` | The current group schedule used in any criteria is removed from the service settings. |
| `19707` | User is removed from the department of the old group. |
| `19708` | User is changed to use the default communication barring profile of the new group. |
| `19709` | The communication barring profile of the user is assigned to the new group: {0}. |
| `19710` | The charge number for the user is removed. |
| `19711` | The disabled FACs for the user are removed because they are not available in the new group. |
| `19712` | User is removed from trunk group. |
| `19713` | The extension of the user is reset to empty due to either the length is out of bounds of the new group, or the extension is already taken in new group. |
| `19714` | The extension of the following alternate number is reset to empty due to either the length out of bounds of the new group or the extension is already taken in new group: {0}. |
| `19715` | The collaborate room using current group default collaborate bridge is moved to the default collaborate bridge of the new group. |
| `19716` | Previously stored voice messages of the user are no longer available. The new voice message will be stored on the mail server of the new group. |
| `19717` | The primary number, alternate numbers or fax messaging number of the user are assigned to the new group: {0}. |
| `19718` | Following domains are assigned to the new group: {0}. |
| `19719` | The NCOS of the user is assigned to the new group: {0}. |
| `19720` | The office zone of the user is assigned to the new group: {0}. |
| `19721` | The announcement media files are relocated to the new group directory. |
| `19722` | User CLID number is set to use the new group CLID number: {0}. |
| `19723` | New group CLID number is not configured. |
| `19724` | The group level announcement file(s) are removed from the user's music on hold settings. |
| `25388` | Target Location Does not Have Vendor Configured. Call Recording for user will be disabled |
| `25389` | Call Recording Vendor for user will be changed from:{0} to:{1} |
| `25390` | Dub point of user is moved to new external group |
| `25391` | Error Occurred while moving Call recording Settings to new location |
| `25392` | Error Occurred while checking for Possible Call Recording Impact. |
| `25393` | Sending Billing Notification Failed |
