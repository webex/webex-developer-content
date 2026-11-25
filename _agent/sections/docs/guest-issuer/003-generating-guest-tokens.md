---
type: Excerpt
canonical_url: https://developer.webex.com/docs/guest-issuer
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Generating Guest Tokens
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/guest-issuer). [Full Markdown](../../../../docs/guest-issuer.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Guest Issuer applications give guest users temporary access to users within your organization. Guest Issuer app creation has been removed—use [Service App Guest Management](https://developer.webex.com/docs/sa-guest-management) for new integrations, or follow [Guest Issuer Migration Guide](https://developer.webex.com/docs/guest-issuer-migration) if you have an existing legacy issuer.

## Selected section

## Generating Guest Tokens

With an existing Guest Issuer app in [My Webex Apps](https://developer.webex.com/my-apps), you can create guest tokens to authenticate guest users and perform actions against the Webex REST API.

Guest tokens use the [JSON Web Token (JWT)](https://en.wikipedia.org/wiki/JSON_Web_Token) standard. JSON Web Tokens are composed of three parts, separated by a dot (`.`):

- Header
- Payload
- Signature

### Header

```json
{
  "typ": "JWT",
  "alg": "HS256"
}
```

The header describes the token:



| Claim   | Value                                     |
| ------- | ----------------------------------------- |
| `typ`   | The *type* of token. Must be `JWT`.       |
| `alg`   | The signature algorithm. Must be `HS256`. |

The header is base64url encoded to create the first part of the token.

### Payload

```json
{
  "sub": "guest-user-7349",
  "name": "Guest User's Display Name",
  "iss": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi85NmFiYzJhYS0zZGNjLTExZTUtYTE1Mi1mZTM0ODE5Y2RjOWE",
  "exp": "1511286849"
}
```

The payload contains the claims for the token. The Webex REST API expects the following claims:



| Claim  | Value                                                                                                                                                                                                                                                         |
| ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `sub`  | The *subject* of the token. This is your unique and public identifier for the guest user. This claim may contain only letters, numbers, and hyphens. This claim is required.                                                                                  |
| `name` | The *display name* of the guest user. This will be the name shown in Webex clients.                                                                                                                                                                     |
| `iss`  | The *issuer* of the token. Use the Guest Issuer ID provided in My Webex Apps. This claim is required.                                                                                                                                                   |
| `exp`  | The *expiration* time of the token, as a [UNIX timestamp](https://en.wikipedia.org/wiki/Unix_time) in seconds. Use the lowest practical value for the use of the token. This is not the expiration time for the guest user's session. This claim is required. |

The payload is then base64url encoded to create the second part of the token.

### Signature

To create the signature, the encoded header and payload, along with the secret (provided when the app is created) are combined and signed using the algorithm specified in the header. For example:

```javascript
var encodedData = base64urlEncode(header) + '.' + base64urlEncode(payload);
var secret = Buffer.from(process.env.GUEST_ISSUER_SECRET, 'base64');
HMACSHA256(encodedData, secret);
```

After creating the signature, all three parts are combined to create the guest token:

```text
ABC123.DEF456.xd84f342d2
```

The secret provided when the app is created is base64-encoded. Certain JWT libraries require a decoded secret to generate the token. For example, to sign a token when using the [jsonwebtoken](https://www.npmjs.com/package/jsonwebtoken) NPM package, create a new `Buffer` to decode the secret when creating the signature:

```javascript
var jwt = require('jsonwebtoken');

var payload = {
  "sub": "guest-user-7349",
  "name": "Guest User's Display Name",
  "iss": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi85NmFiYzJhYS0zZGNjLTExZTUtYTE1Mi1mZTM0ODE5Y2RjOWE"
};

var token = jwt.sign(
  payload,
  Buffer.from(process.env.GUEST_ISSUER_SECRET, 'base64'),
  { expiresIn: '1h' }
);
```

### More Resources

[JWT.io](https://jwt.io) provides an interactive JWT debugger and a great list of libraries which can be used to generate JSON Web Tokens in different languages. [More tools](https://github.com/CiscoDevNet/awesome-webex#tools) are also available to help generate guest tokens.
