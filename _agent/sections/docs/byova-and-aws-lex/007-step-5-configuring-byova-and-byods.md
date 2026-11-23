---
type: Excerpt
canonical_url: https://developer.webex.com/docs/byova-and-aws-lex
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Step 5: Configuring BYOVA and BYODS'
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/byova-and-aws-lex). [Full Markdown](../../../../docs/byova-and-aws-lex.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](002-prerequisites.md)

## Article introduction

Transform your contact center with intelligent voice interactions using Webex Contact Center's BYOVA (Bring Your Own Virtual Agent) feature and AWS Lex.

## Selected section

## Step 5: Configuring BYOVA and BYODS

### 5.1 Understanding BYOVA and BYODS

- **BYOVA (Bring Your Own Virtual Agent)**: Allows you to integrate external AI services as virtual agents
- **BYODS (Bring Your Own Data Source)**: Enables integration with external data sources for enhanced AI capabilities
  - BYOVA builds on top of the BYODS framework
  - Provides secure, standardized data exchange between Webex and third-party providers
  - Uses JWS (JSON Web Signature) tokens for authentication
  - Requires Service App creation and admin authorization

**Important**: BYOVA requires BYODS setup first, as the virtual agent configuration depends on having a registered data source.

### 5.2 Create a Service App for BYODS

Before configuring BYOVA, we need to set up a Service App for data source integration, as BYOVA builds on top of the BYODS (Bring Your Own Data Source) framework.

> **Prerequisite**: You need your public URL from Step 3 for the domain configuration.

1. **Navigate to Webex Developer Portal**
   - Go to [developer.webex.com](https://developer.webex.com)
   - Sign in with your Webex account

2. **Create a New Service App**
   - Go to **My Apps** → **Create a New App**
   - Choose **Service App** as the application type

3. **Configure the Service App**
   - **App Name**: `BYOVA Gateway Service App` (or your preferred name)
   - **Icon**: Choose a suitable icon for your app or upload your own
   - **Description**: Enter a brief description of your app
   - **Contact Email**: Enter your admin email address
   - **Scopes**: Ensure you select:
     - `spark-admin:datasource_read`
     - `spark-admin:datasource_write`
   - **Domains**: Enter your gateway domain from Step 3
     - **Format**: Domain only (no `https://` or port)
     - **ngrok example**: `abc123def456.ngrok-free.app`
     - **Production example**: `byova-gateway.yourcompany.com`
     - ✅ Correct: `abc123.ngrok-free.app`
     - ❌ Wrong: `https://abc123.ngrok-free.app`
     - ❌ Wrong: `abc123.ngrok-free.app:50051`
   - **Data Exchange Schema**: Select `VA_service_schema` for voice virtual agent interactions
     - This schema (ID: `5397013b-7920-4ffc-807c-e8a3e0a18f43`) is specifically designed for voice virtual agent services
     - Reference: [VoiceVirtualAgent Schema](https://github.com/webex/dataSourceSchemas/tree/v1.10/Services/VoiceVirtualAgent/5397013b-7920-4ffc-807c-e8a3e0a18f43)
   - Complete any other required information


4. **Save the Service App Client ID and Client Secret**
   - Under **Authentication**, locate the **Client ID** and **Client Secret**
   - Save these credentials for later use

5. **Submit for Admin Approval**
   - In your sandbox, select **"Request Admin Approval"**
   - This makes the Service App visible in Control Hub for admin authorization

### 5.3 Register Your Data Source

1. **Get Admin Authorization**
   - In Control Hub (admin.webex.com), navigate to **Apps** → **Service Apps**
   - Find your Service App and click **"Authorize"**
   - This generates org-specific access and refresh tokens

2. **Get Service App Token**
   - After admin approval, return to [developer.webex.com](https://developer.webex.com)
   - Go to **My Apps** and select your Service App
   - Under **Org Authorizations**, locate your org in the list and select it
   - Paste the **Client Secret** from step 1 into the **Client Secret** field and click **"Generate Tokens"**
   - Save the returned `access_token` - you'll need it to register your data source
   - Note: Tokens expire and will need to be refreshed using the refresh token provided

3. **Register the Data Source**

   Use the access token from step 2 to register your data source with the BYoDS API.

   **API Reference**: [Register a Data Source](https://developer.webex.com/admin/docs/api/v1/data-sources/register-a-data-source)

   **Request body**:

   ```json
   {
     "schemaId": "5397013b-7920-4ffc-807c-e8a3e0a18f43",
     "url": "https://YOUR_PUBLIC_URL",
     "audience": "BYOVAGateway",
     "subject": "callAudioData",
     "nonce": "123456",
     "tokenLifetimeMinutes": "1440"
   }
   ```

   **Critical - URL Matching**:

   - The `url` field MUST exactly match `jwt_validation.datasource_url` from Step 4.2
   - Use the same format: `https://your-domain` (no port number)
   - Examples:
     - ngrok: `https://abc123def456.ngrok-free.app`
     - production: `https://byova-gateway.yourcompany.com`

   **Common Mistakes** (all cause JWT validation to fail):

   - ❌ Gateway config: `https://example.com` / BYoDS: `https://example.com:443`
   - ❌ Gateway config: `https://example.com` / BYoDS: `https://example.com:50051`
   - ✅ Gateway config: `https://example.com` / BYoDS: `https://example.com`

   **After registration**:

   - Save the `datasource ID` from the API response
   - You'll use this in the next section (5.4)


**Reference**: For detailed BYODS setup instructions, see the [Bring Your Own Data Source documentation](https://developer.webex.com/create/docs/bring-your-own-datasource).

### 5.4 Configure BYOVA Virtual Agent

1. **Navigate to Virtual Agents**
   - In Control Hub, go to **Contact Center** → **Integrations** → **Features**
   - Click **"Create Feature"**

2. **Configure Virtual Agent Settings**
   - **Name**: `AWS Lex Virtual Agent`
   - **Type of Connector**: Select **"Service App"**
   - **Authorized Service App**: Select your Service App from step 5.2
   - **Resource Identifier**: Enter the datasource ID you saved in step 5.3
   - Click **"Create"**

---
