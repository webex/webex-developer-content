---
type: Article
title: Webex Postman Collection Reaches GA Plus New OpenAPI Specs Repository
canonical_url: https://developer.webex.com/blog/webex-postman-collection-reaches-ga-plus-new-openapi-specs-repository
content_type: blog
date: '2026-05-04'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/webex-postman-collection-reaches-ga-plus-new-openapi-specs-repository)

### What's New: GA Release

The Webex Postman Collection has been battle-tested by developers worldwide over the past several months. Based on your feedback, we've refined the collections, improved documentation, and ensured rock-solid reliability. Today's GA release means you can confidently integrate these collections into your production workflows.

**What you get with the Postman Workspace:**

- **Complete API coverage** - Every Webex API organized into logical collections (Messaging, Meetings, Calling, Contact Center, and more)
- **Pre-configured environments** - US, EU, and APAC regional endpoints ready to use (Webex runs in multiple regions; choose the environment that matches where your organization is hosted)
- **Built-in examples** - Real request/response samples for every endpoint
- **Automated tests** - Collection-level tests to validate API responses
- **Always up-to-date** - Generated directly from our OpenAPI specs, synced regularly

If you're already using the workspace, nothing changes—you're already on the GA release. If you're new to Postman or haven't explored our collections yet, check out our [previous blog post](https://developer.webex.com/blog/announcing-the-official-webex-postman-workspace) for a complete getting-started guide.

### New: OpenAPI Specifications Repository

For developers who work beyond Postman—those building SDKs, API testing frameworks, documentation sites, or custom tooling—we've published the complete OpenAPI specifications that power our Postman collections.

**Repository:** [github.com/webex/webex-openapi-specs](https://github.com/webex/webex-openapi-specs)

### What's Inside

The repository contains OpenAPI 3.0 specifications for all Webex public APIs, organized by functional area:

```
webex-openapi-specs/
├── messaging.yaml          # Spaces, messages, teams, webhooks
├── meetings.yaml           # Meetings, recordings, participants
├── calling.yaml            # Webex Calling features
├── devices.yaml            # Device management and xAPI
├── contact-center.yaml     # Contact Center APIs
├── admin.yaml              # Organization and user management
└── ...
```

**Common starting points:**
- Building a chat bot or integration? Start with `messaging.yaml`
- Working with meetings or recordings? Use `meetings.yaml`
- Managing users or organizations? Check `admin.yaml`

<br/>

Each specification includes:

- Complete endpoint definitions (paths, methods, parameters)
- Request/response schemas with examples
- Authentication requirements
- Rate limiting information
- Webhook payload schemas where applicable

<br/>

### Why OpenAPI?

OpenAPI (formerly Swagger) is the industry standard for describing REST APIs. Having these specs in a public repository unlocks several powerful workflows:

**Generate client SDKs** - Use tools like [OpenAPI Generator](https://openapi-generator.tech/) or [Swagger Codegen](https://swagger.io/tools/swagger-codegen/) to create type-safe clients in your language of choice:

```bash
# Example: Generate a Python client
openapi-generator-cli generate \
  -i https://raw.githubusercontent.com/webex/webex-openapi-specs/main/messaging.yaml \
  -g python \
  -o ./webex-messaging-client
```

**Import into any API tool** - Beyond Postman, you can import these specs into Insomnia, Bruno, REST Client for VS Code, or any OpenAPI-compatible tool.

**Use Bruno for offline-first API testing** - [Bruno](https://www.usebruno.com/) is an open-source API client that stores collections directly in your filesystem (no cloud required). You have two options for working with Webex APIs in Bruno:

*Option 1: Import from URL*
1. In Bruno, create a new collection or open an existing one
2. Right-click the collection → **Import** → **OpenAPI v3 Spec**
3. Choose **From URL** and paste:
   ```
   https://raw.githubusercontent.com/webex/webex-openapi-specs/main/messaging.yaml
   ```

*Option 2: Clone and work locally*
```bash
git clone https://github.com/webex/webex-openapi-specs.git
cd webex-openapi-specs
# In Bruno: Import → OpenAPI v3 Spec → From File → select messaging.yaml
```

Bruno's Git-friendly approach means your entire team can share API collections through your existing repository workflow, with full diff history and code review for API test changes.

**Build custom documentation** - Generate API reference docs tailored to your team's needs using tools like [Redoc](https://redocly.com/redoc) or [Stoplight Elements](https://stoplight.io/open-source/elements).

**Validate requests programmatically** - Use the schemas for request validation in your own applications or test suites.

**Mock servers** - Spin up mock API servers for frontend development or integration testing without hitting production endpoints.

### Keeping In Sync

The OpenAPI specs in this repository are the source of truth for our Postman collections and are part of our official publishing pipeline. When we update an API—adding new endpoints, deprecating old ones, or changing parameters—the specs are updated through the same process that publishes to [developer.webex.com](https://developer.webex.com). The Postman collections then automatically rebuild from these specs.

This means the specs in the repository are always in sync with what you see documented on developer.webex.com. Whether you're using Postman, consuming the specs directly, or reading the docs on the portal, you're always working with the same, authoritative API definitions.

### For Teams Using Multiple Tools

One of the most common pain points we hear from teams is maintaining consistency across different API testing and development tools. Developers use Postman, QA uses something else, automation uses yet another tool, and keeping everything in sync becomes a maintenance nightmare.

With the OpenAPI specs repository, your entire team can work from the same source of truth:

- **API explorers** fork the Postman collection
- **SDK developers** generate clients from the OpenAPI specs
- **QA automation** imports specs into their testing framework
- **Documentation writers** generate reference docs from the same specs

Everyone stays aligned because everyone's using the same definitions.

### Getting Started

#### Prerequisites: Get Your Access Token

Before you can make API calls, you'll need a Webex access token:

1. Sign up for a free Webex account at [developer.webex.com](https://developer.webex.com) (if you don't have one)
2. Log in to the developer portal
3. Your personal access token will be displayed on the documentation pages, or visit the [Getting Started guide](https://developer.webex.com/docs/getting-started) to generate one

This token authenticates all your API requests. Keep it secure—treat it like a password.

#### Using Postman

1. Visit the **[Webex Public Workspace](https://www.postman.com/webexdev/webex-public-workspace/)**
2. Fork the collection you need into your workspace
3. Set up your authentication token (add it to the environment or collection variables)
4. Start making requests

For a detailed walkthrough, see our [Postman getting started guide](https://developer.webex.com/blog/announcing-the-official-webex-postman-workspace).

#### Quick Test: Your First API Call

Verify your setup with a simple API call to get your own user details:

**Using Postman or Bruno:**
- Method: `GET`
- URL: `https://webexapis.com/v1/people/me`
- Headers: `Authorization: Bearer YOUR_ACCESS_TOKEN`

**Using curl:**
```bash
curl -X GET "https://webexapis.com/v1/people/me" \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN"
```

You should receive a JSON response with your user profile. If this works, you're ready to explore the rest of the Webex APIs!

#### Using OpenAPI Specs Directly

1. Browse the **[webex-openapi-specs repository](https://github.com/webex/webex-openapi-specs)**
2. Download or reference the spec file you need
3. Import into your tool of choice or use with code generators

The repository README includes examples for common workflows like SDK generation, importing into different tools, and setting up mock servers.

### Resources

- **Postman Workspace:** [postman.com/webexdev/webex-public-workspace](https://www.postman.com/webexdev/webex-public-workspace/)
- **OpenAPI Specs Repository:** [github.com/webex/webex-openapi-specs](https://github.com/webex/webex-openapi-specs)
- **Webex API Documentation:** [developer.webex.com](https://developer.webex.com/)
- **Getting Started with Postman:** [Previous blog post](https://developer.webex.com/blog/announcing-the-official-webex-postman-workspace)

Whether you're building your first Webex integration or maintaining production applications at scale, these resources are designed to help you ship faster and with more confidence. Fork the collection, clone the repo, and start building.

Happy coding!
