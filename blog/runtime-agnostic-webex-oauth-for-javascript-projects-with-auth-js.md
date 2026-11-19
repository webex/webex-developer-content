---
type: Article
title: Runtime Agnostic Webex OAuth for JavaScript Projects with Auth.js
canonical_url: https://developer.webex.com/blog/runtime-agnostic-webex-oauth-for-javascript-projects-with-auth-js
content_type: blog
date: '2024-07-15'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/runtime-agnostic-webex-oauth-for-javascript-projects-with-auth-js)

[Auth.js](https://authjs.dev/) (previously NextAuth.js) is an open-source authentication solution tailored for JavaScript web applications, boasting essential security features such as server-only cookies, CSRF protection, and encrypted JWT sessions. Its current iteration includes built-in OAuth support for over 82 prominent services, including Webex, and offers compatibility with 23 databases/ORMs like MySQL, Postgres, Prisma, Drizzle, and MikroORM. Moreover, Auth.js exhibits versatility across different runtimes such as Node.js, Deno, Bunt, and Serverless, while seamlessly integrating with popular frameworks like Next.js, SolidStart, and SvelteKit.

These combined attributes make it an exceptionally developer-friendly choice for JavaScript applications requiring OAuth functionality. In this post, we'll guide you through setting up Auth.js in a TypeScript SvelteKit project for Webex OAuth. Note that as of this writing, SvelteKit support in Auth.js is experimental. Please refer to the [documentation](https://authjs.dev/reference/sveltekit) before replicating anything.

### Installation

If you do not have an existing [SvelteKit](https://kit.svelte.dev/) project, create one using `create-svelte` as shown below:

```bash
npm create svelte@latest authjs-webex-oauth
```

#### Setting Environment Variables

To set up environment variables for your Webex integration, follow these steps:

1. **Register Your Integration**: Refer to the [Registering your Integration on Webex](https://developer.webex.com/docs/integrations#registering-your-integration) guide. Note down your Client ID and Client Secret provided during registration.

2. **Create `.env` File**: Create a `.env` file in the root directory of your project if it doesn't exist already.

3. **Assign Variables**:
    - Set `WEBEX_CLIENT_ID` to your Webex Client ID obtained from the Webex developer portal.
    - Set `WEBEX_CLIENT_SECRET` to your Webex Client Secret obtained during integration registration.
    - Define `WEBEX_SCOPE` with the required scopes for your integration. Include at minimum `spark:kms` and `spark:people_read`.
    - Generate a random 64-character string and assign it to `AUTH_SECRET` in the `.env` file for secure session management.

Example `.env` file:

```bash
WEBEX_CLIENT_ID=your_webex_client_id
WEBEX_CLIENT_SECRET=your_webex_client_secret
WEBEX_SCOPE=spark:kms spark:people_read
AUTH_SECRET=random_64_character_long_string
```

Ensure these variables are securely managed and not exposed in version control or publicly accessible locations.

#### Add the Package

Inside the project directory (i.e., `authjs-webex-oauth` here), add the Auth.js package as a project dependency:

```bash
npm install @auth/sveltekit
```

#### Add a New Authentication Handler

Create a new handler under `src/lib/server/handlers/authentication.ts`:

```javascript
import { SvelteKitAuth } from '@auth/sveltekit';
import Webex from '@auth/sveltekit/providers/webex';
import {
  AUTH_SECRET,
  WEBEX_CLIENT_ID,
  WEBEX_CLIENT_SECRET,
  WEBEX_SCOPE
} from '$env/static/private';

const { handle, signIn, signOut } = SvelteKitAuth(async (event) => {
  return {
    secret: AUTH_SECRET,
    providers: [
      Webex({
        style: { logo: '/webex.svg', bg: '#fff', text: '#000' },
        clientId: WEBEX_CLIENT_ID,
        clientSecret: WEBEX_CLIENT_SECRET,
        authorization: { params: { prompt: 'select_account', scope: WEBEX_SCOPE } }
      })
    ]
  };
});

export const authentication = handle;
export { signIn, signOut };
```

#### Add a New Authorization Handler

Create a new handler under `src/lib/server/handlers/authorization.ts`:

```javascript
import type { Handle } from '@sveltejs/kit';
import { redirect } from '@sveltejs/kit';

export const authorization: Handle = async ({ event, resolve }) => {
    // Protect any routes under /authenticated
    if (event.url.pathname.startsWith('/authenticated')) {
        const session = await event.locals.auth();
        
        if (!session) {
            // Redirect to the signin page
            throw redirect(303, '/auth/signin');
        }
    }

    // If the request is still here, just proceed as normal
    return resolve(event);
};
```

#### Add a Hook Sequence

Modify or add the server-side hooks file at `src/hooks.server.ts`.

```javascript
import type { Handle } from '@sveltejs/kit';
import { sequence } from '@sveltejs/kit/hooks';
import { authentication as authenticationHandle } from '$lib/server/handlers/authentication';
import { authorization as authorizationHandle } from '$lib/server/handlers/authorization';

export const handle: Handle = sequence(authenticationHandle, authorizationHandle);
```

### Usage

Once configured, any routes prefixed with `/authenticated` will automatically benefit from the protection provided by the handle hook. To verify functionality, navigate to any route in your running application (`npm run dev`).

You have the flexibility to extend the sequence with additional middleware-like functions and implement more sophisticated authorization logic within the respective handler files. The current setup establishes authorization based on paths, but an alternative per-component approach is also viable and can complement or replace path-based techniques.

Note that Auth.js utilizes JWT by default for session storage in the absence of a configured database adapter. For enhanced session management, consider integrating your preferred [database adapter](https://authjs.dev/getting-started/database) on the server side.

### Wrapping Up

This article provided a brief overview of the new Auth.js package for Webex OAuth. JavaScript project owners are encouraged to use this package to simplify their workload when authenticating with Webex. To explore other community offerings or learn more about our developer platform, please visit [Webex Developers](https://developer.webex.com/docs/).
