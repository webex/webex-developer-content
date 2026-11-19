---
type: Guide
title: Audit Events API Response Error Codes Reference | Consolidated Guide
display_title: Audit Events Error Reference
canonical_url: https://developer.webex.com/docs/audit-events-api-response-error-codes-reference
content_type: documentation
product_group:
- webex-suite
categories:
- admin
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/audit-events-api-response-error-codes-reference)

Reference listing of possible error codes for the Audit Events API.

---

The following error codes may appear in `GET /v1/adminAudit/events` API response when change notification-based user provisioning fails with Webex Calling license. The table provides the reason for the error:



| Error Code | Description |
|---|--|
| WXC-4201 | WXC-4201: The phone number is already in use.  |
| WXC-4202 | WXC-4202: The Extension is already in use. |
| WXC-4410 | WXC-4410: Invalid phone number. A phone number used for incoming calls must contain only the characters +, - and 0-9. Only the leading character may be a +. |
| WXC-4801 | WXC-4801: Invalid email address. The email address can contain only one @ and A-Z, a-z, 0-9, ! # $ % & * + - / =  _ '{' '}' | ~ . ? ^ or single quotes. |
| WXC-4802 | WXC-4802: Invalid email address. The email address must contain an @ symbol. |
| WXC-4803 | WXC-4803: Invalid email address. The email address cannot contain two @ symbols. |
| WXC-4805 | WXC-4805: Mobile Network integration is not configured for this user. |
| WXC-4900 | WXC-4900: Invalid email address. The username length cannot be greater than 161 characters long and must be in username@domain format. |
| WXC-4901 | WXC-4901: Invalid email address. The supported characters in the email can be a letter, a digit, a single quote, or one of the following characters: # @ $ % & + - / = ? ; . | _ ~ ! \ ` ^ '{' '}'. |
| WXC-4909 | WXC-4909: Invalid extension/ extension length. |
| WXC-4910 | WXC-4910: Invalid extension. The extension can only contain characters from 0-9. |
| WXC-4911 | WXC-4911: Invalid extension. The extension cannot be an emergency number. |
| WXC-4912 | WXC-4912: Invalid extension. The extension cannot be a repair call number. |
| WXC-4942 | WXC-4942: Invalid extension. |
| WXC-4982 | WXC-4982: Invalid phone number length. |
| WXC-4989 | WXC-4989: Invalid email address. Ensure the email address is in username@domain format. |
| WXC-4992 | WXC-4992: Invalid domain name in email. Numeric IP address is not allowed in the domain name. |
| WXC-4993 | WXC-4993: Invalid domain name in email. Domain name cannot end with the . character. |
| WXC-4997 | WXC-4997: Invalid domain name in email. Domain name may only contain letter, digit, ., -, : and square brackets. |
| WXC-25058 | WXC-25058: Extension cannot be less than 2 or greater than 6 characters. |
| WXC-25279 | WXC-25279: Invalid field for firstName or lastName. It cannot have %, #, <, >, backslash, forward slash, and quote characters. |
| WXC-25400 | WXC-25400: firstName cannot be less than 1 or greater than 30. |
| WXC-25401 | WXC-25401: lastName cannot be less than 1 or greater than 30. |
| WXC-25402 | WXC-25402: Email cannot be longer than 161 characters. |
| WXC-25404 | WXC-25404: Webex calling features are undergoing maintenance and are temporarily unavailable. Try again later. |
| WXC-27392 | WXC-27392: The Mobile Network Integration is not enabled. |
| WXC-27516 | WXC-27516: Do not set the User to use custom caller ID name for external calls when custom caller ID name is empty. |
| WXC-27517 | WXC-27517: Do not set the User to use location caller ID name for external calls when location caller ID name is empty. |
| WXC-27590 | WXC-27590: Activate the number to convert to ESim. |
| WXC-27593 | WXC-27593: Cannot remove the main number of the user while an ESim device is associated to the user. |
| WXC-27771 | WXC-27771: Assigning Restricted Non-Geographical number as primary, alternate, or fax number is not allowed. |
| WXC-500 | WXC-500: An unexpected condition prevented the request from completing. Please try again. |
| WXC-BIFROST-U400401 | WXC-400401: Unable to determine the Webex Calling location to add the user. |
| WXC-BIFROST-U400405 | WXC-500: An unexpected condition prevented the request from completing. Please try again. |
| WXC-BIFROST-U400406 | WXC-500: An unexpected condition prevented the request from completing. Please try again. |
| WXC-BIFROST-U400407 | WXC-500: An unexpected condition prevented the request from completing. Please try again. |
| WXC-BIFROST-U400408 | WXC-500: An unexpected condition prevented the request from completing. Please try again. |
