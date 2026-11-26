---
type: Excerpt
canonical_url: https://developer.webex.com/docs/basics
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- API Errors
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/basics). [Full Markdown](../../../../docs/basics.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

While working with the Webex REST API is easy, there are a few things we standardize on throughout the API, such as pagination of long result sets or HTTP response codes.

## Selected section

## API Errors

The Webex API returns standard HTTP status codes for request responses. If an error occurs, more information will be provided in the response.

### HTTP Response Codes

The list below describes the common success and error responses you should expect from the API:



| Code                                       | Status                 | Description                                                                                                                                                                                                                          |
| ------------------------------------------ | ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 200 | OK                     | Successful request with body content.                                                                                                                                                                                                |
| 201 | Created                | The request has succeeded and has led to the creation of a resource.                                                                                                                                                                 |
| 202 | Accepted               | The request has been accepted for processing.                                                                                                                                                                                        | 
| 204 | No Content             | Successful request without body content.                                                                                                                                                                                             |
| 400 | Bad Request            | The request was invalid or cannot be otherwise served. An accompanying error message will explain further.                                                                                                                           |
| 401 | Unauthorized           | Authentication credentials were missing or incorrect.                                                                                                                                                                                |
| 403 | Forbidden              | The request is understood, but it has been refused or access is not allowed.                                                                                                                                                         |
| 404 | Not Found              | The URI requested is invalid or the resource requested, such as a user, does not exist. Also returned when the requested format is not supported by the requested method.                                                            |
| 405 | Method Not Allowed     | The request was made to a resource using an HTTP request method that is not supported.                                                                                                                                               |
| 409 | Conflict               | The request could not be processed because it conflicts with some established rule of the system. For example, a person may not be added to a room more than once.                                                                   |
| 410 | Gone                   | The requested resource is no longer available.                                                                                                                                                                                       |
| 415 | Unsupported Media Type | The request was made to a resource without specifying a media type or used a media type that is not supported.                                                                                                                       |
| 423 | Locked                 | The requested resource is temporarily unavailable. A `Retry-After` header may be present that specifies how many seconds you need to wait before attempting the request again.                                                       |
| 428 | Precondition Required | File(s) cannot be scanned for malware and need to be force downloaded.              
| 429 | Too Many Requests      | Too many requests have been sent in a given amount of time and the request has been rate limited. A `Retry-After` header should be present that specifies how many seconds you need to wait before a successful request can be made. |
| 500 | Internal Server Error  | Something went wrong on the server. If the issue persists, feel free to contact the [Webex Developer Support team](https://developer.webex.com/support).                                                                                                        |
| 502 | Bad Gateway            | The server received an invalid response from an upstream server while processing the request. Try again later.                                                                                                                       |
| 503 | Service Unavailable    | Server is overloaded with requests. Try again later.                                                                                                                                                                                 |
| 504 | Gateway Timeout | An upstream server failed to respond on time. If your query uses `max` parameter, please try to reduce it.                                                                                                                                                                                 |

### Responses with Errors

When retrieving multiple resources from the API, such as listing multiple Rooms or People, individual resources which should be included in the response may not be included because of an error. If any partial failures occur, the API will respond with a 200 OK and the response body will contain the entire list of resources, including the individual resources which could not be retrieved.

Resources which encounter errors during retrieval will include an `errors` object. This `errors` object will contain a specific error `code` and `reason` describing why the individual resource could not be returned in the request. Failures encountered during the request may be the result of a temporary issue, such as the inability to contact an on-premise key management server in a timely manner, or something more permanent. The error code and description will provide more detail about the error.

The `errors` object should only be present in the response if at least one resource could not be retrieved.

#### Example Response with Errors

The sample JSON below demonstrates how an error encountered while retrieving one room in a list of rooms is presented:

```json
{
  "items": [
    {
      "id": "Y2lzY29zcGFyazovL3VzL1JPT00vYmJjZWIxYWQtNDNmMS0zYjU4LTkxNDctZjE0YmIwYzRkMTU0",
      "title": "Project Unicorn - Sprint 0",
      "type": "group",
      "isLocked": true,
      "teamId": "Y2lzY29zcGFyazovL3VzL1JPT00vNjRlNDVhZTAtYzQ2Yi0xMWU1LTlkZjktMGQ0MWUzNDIxOTcz",
      "lastActivity": "2016-04-21T19:12:48.920Z",
      "created": "2016-04-21T19:01:55.966Z"
    },
    {
      "id": "Y2lzY29zcGFyazovL3VzL1JPT00vNTIxN0EyMzYtNDQzQi00NThELTkzNjAtRDRFOTMyMTBBNUU5",
      "title": "eyJhbGciOiIiLCJraWQiOiIiLCJlbmMiOiIifQ....",
      "errors": {
        "title": {
          "code": "kms_failure",
          "reason": "Key management server failed to respond appropriately. For more information: https://developer.ciscospark.com/errors.html"
        }
      }
    }
  ]
}
```

#### Error Codes

The following table describes the errors which may be returned by the API:



| Code          | Reason                                                 | Description                                                                                                                                                                                                                  |
| ------------- | ------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `kms_failure` | Key management server failed to respond appropriately. | The Webex API is unable to contact the appropriate encryption key management server (KMS), or the KMS did not respond in a timely manner, and could not retrieve the requested resource. Try your request again later. |

### SSL Connection Errors

The Webex API uses the [Server Name Indication (SNI)](https://en.wikipedia.org/wiki/Server_Name_Indication) extension to TLS/SSL. If your SSL client fails to connect to the API with an error such as `hostname 'webexapis.com' doesn't match either of '*.wbx2.com', 'wbx2.com'`, your client may not support SNI. Verify that your client supports the SNI extension. If your client does not support the SNI extension, then upgrade your client to a version which will support it and try your request again. Never configure your client to ignore SSL connection errors.

SNI support was implemented in these versions of the following common libraries and tools:

- Java 1.7
- PHP 5.3
- Python 2.7.9, Python 3
- Ruby (net/http) 2.0
- cURL 7.18.1
- wget 1.14
