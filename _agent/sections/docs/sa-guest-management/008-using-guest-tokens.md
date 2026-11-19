---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sa-guest-management
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Using Guest Tokens
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sa-guest-management). [Full Markdown](../../../../docs/sa-guest-management.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Guest Management happens via Service Apps in order to provide unlicensed users with temporary access to Webex functionality. 

## Selected section

## Using Guest Tokens

Once you've created a guest access token, you can use it to authenticate as a guest user and interact with Webex users. The Webex SDK and Webex REST APIs accept the guest `Access Token`. See below for a few examples of using a guest token with our SDKs and the API.

When a guest token with a new subject is retrieved, the guest is created, and the guest can then perform actions just like regular users, albeit with limited scope. There are a few important differences from regular users to keep in mind:

- You can only create the guest implicitly by retrieving the token. You cannot use the `/people` API or Control Hub.
- Guest users may only interact with regular users; they cannot interact with other guest users
- Guests now have a `personId` and synthetic `email` that you can use in API calls.

Session management is handled automatically when using guest tokens with the SDKs and Widgets.

### Using the SDKs

To use the guest `accessToken` with the SDKs, all you need to do is pass it in the `init` function.

```js
 webex = window.webex = Webex.init({
    config: generateWebexConfig({}),
    credentials: {
      access_token: accessToken
    }
  });
```



> **Info**
>
> Previously, you needed to exchange a JWT token for an Access Token. This is not needed any longer.



To quickly test a guest token with a widget, use the [Widgets Demo](https://code.s4d.io/widget-demo/production/index.html).
