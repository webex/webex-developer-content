---
type: Excerpt
canonical_url: https://developer.webex.com/docs/rest-api-basics
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Rate Limiting
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/rest-api-basics). [Full Markdown](../../../../docs/rest-api-basics.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This tutorial describes the basics of consuming a REST API - namely the Webex API, as well as how to use Postman to explore a REST API.

## Selected section

## Rate Limiting

The Webex API rate limits requests to maintain appropriate service levels for all Webex API users. The rate limiting policies in place are fine-grained and often overlap and are therefore too complex to document exactly. The following provides general information for handling rate limiting errors, as well as upper limits for commonly used API use cases. It also provides recommendations for running and automating large API workloads.

- [Handling 429 Errors](https://developer.webex.com/docs/basics#handling-429-errors)
- [Upper Limits for API Requests](https://developer.webex.com/docs/basics#upper-limits-for-api-requests)
- [Recommendations for Large API Workloads](https://developer.webex.com/docs/basics#recommendations-for-large-api-workloads)

<a id="handling-429-errors"></a>

### Handling 429 Errors

If your application hits an API rate limit, the Webex API gateway returns a `429 Too Many Requests` response. The response includes a `Retry-After` header indicating how long your application must wait before making another request to the same endpoint. For example, the following is an example 429 response indicating that the application should wait 3600 seconds before retrying the request.

```bash
HTTP/1.1 429 Too Many Requests\
Content-Type: text/html\
Retry-After: 3600
```

See the [RetryAfterDemo code repository](https://github.com/webex/SparkRetryAfterDemo) on GitHub for a detailed example of handling 429 errors in Python.

<a id="upper-limits-for-api-requests"></a>

### Upper Limits for API Requests

Most of our REST APIs enforce a rate limit of around 300 requests per minute, with the `/people` and `/messages` APIs providing a higher quota that is dynamically adjusted.

<a id="recommendations-for-large-api-workloads"></a>

### Recommendations for Large API Workloads

This section contains recommendations for applications that make a large number of API calls, or make API calls over a broad range of APIs.

- **Don't use end-user accounts for large workloads**. Don't use end-user accounts for large workloads as it may affect the user's experience, and they are not guaranteed to work with large workloads that affect a whole organization. For apps that act only on behalf of the user and make a small number of API requests a standard Webex user account can be used. However, for large API workloads it's recommended that you use a dedicated account specifically provisioned for that purpose. For example, [admin accounts](https://developer.webex.com/docs/admin) can be used to schedule meetings on behalf of users and should be dedicated to the API flow to reduce the probability of exceeding the allowed quota.

- **Bot accounts**. If using an admin account is not possible consider using a [bot account](https://developer.webex.com/docs/bots), which have less restrictive rate limits than end-user accounts. However, due to content ownership rules with bot accounts, there are known issues when using them to automate certain types of messaging API workloads (for example, creating a very large number of messaging spaces, posting content to those spaces, and updating the members of those spaces). For these scenarios it's recommended that the automated system partition its work across separate accounts (see below).

- **Partition concurrent API workloads across separate users**. API rate limits are shared per user, so multiple API workloads authenticating with the same user will affect each other's API limits. It's recommended that large API workloads be partitioned across separate users for separate concurrent tasks.
