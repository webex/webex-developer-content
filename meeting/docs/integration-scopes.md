---
type: Guide
title: Integration Scopes
display_title: Integration Scopes
canonical_url: https://developer.webex.com/docs/integration-scopes
content_type: documentation
product_group:
- webex-suite
- webex-contact-center
categories:
- admin
- calling
- create
- meeting
- messaging
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/integration-scopes)

Use this reference to select the minimum Webex Suite and Webex Contact Center scopes that your integration needs.

## Select scopes

Scopes limit the resources and operations available to an access token. Select scopes when you [create an integration](https://developer.webex.com/docs/integrations), then request a space-separated subset of those registered scopes during [authentication](https://developer.webex.com/docs/authentication#requesting-permission).

The user authorizing the integration must also have permission to perform the requested operations. Granting an administrative scope does not give a non-administrator access to administrative functions.

## Available scopes

The following list combines the scopes available for Webex Suite and Webex Contact Center integrations.



> **Webex Contact Center scopes**
>
> Many Webex Contact Center scopes use the `cjp:` prefix. Common examples include `cjp:config_read`, `cjp:config_write`, `cjp:task_read`, `cjp:task_write`, and `cjp:user`. Some Contact Center APIs use other scope families, so verify the required scopes in each API reference and request only the scopes your integration needs.





The scope catalog is generated dynamically. View the [official portal page](<https://developer.webex.com/docs/integration-scopes>) for scope names and descriptions.



## Important scope behavior

### Administrative scopes

Scopes beginning with `spark-admin` require a user with administrative access to the organization. Requesting one of these scopes does not elevate the authorizing user's role.

For Webex Contact Center administrator APIs, the authorizing user must have the appropriate Webex Contact Center administrator role in Control Hub. See [Webex Contact Center administrator roles and privileges](https://help.webex.com/en-us/article/n5jdj19/Webex-Contact-Center-administrator-roles-and-privileges).

### Compliance scopes

Scopes beginning with `spark-compliance` require an organization compliance officer. See the [Compliance Guide](https://developer.webex.com/docs/compliance#compliance).

### `spark:all`

The `spark:all` scope grants access to Webex account features that are not covered by other user-level scopes. It does not include `spark-admin` privileges. Some Webex SDK calling features require `spark:all`; most integrations should request narrower scopes.

### `spark:kms`

Webex adds `spark:kms` to an integration's selected scopes so it can interact with encrypted content such as messages. The generated authorization URL includes this scope. If you build the authorization URL yourself, include `spark:kms` when the APIs you call require access to encrypted content.

## Next steps

After selecting scopes, [create the integration](https://developer.webex.com/docs/integrations#create-an-integration) and implement the [OAuth authentication flow](https://developer.webex.com/docs/authentication).
