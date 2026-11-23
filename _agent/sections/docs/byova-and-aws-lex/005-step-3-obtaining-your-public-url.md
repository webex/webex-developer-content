---
type: Excerpt
canonical_url: https://developer.webex.com/docs/byova-and-aws-lex
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Step 3: Obtaining Your Public URL'
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/byova-and-aws-lex). [Full Markdown](../../../../docs/byova-and-aws-lex.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](002-prerequisites.md)

## Article introduction

Transform your contact center with intelligent voice interactions using Webex Contact Center's BYOVA (Bring Your Own Virtual Agent) feature and AWS Lex.

## Selected section

## Step 3: Obtaining Your Public URL

Your gateway needs a publicly accessible HTTPS URL. This URL will be used consistently in:

- Service App domain configuration (Step 5.2)
- BYODS datasource registration (Step 5.3)  
- Gateway JWT configuration (Step 4.2)

**Important**: Use the same URL format everywhere - no port numbers needed!

### URL Format: Simple and Consistent

You'll use your URL in this format throughout the setup:

| Configuration Point | Example URL                        |
|---------------------|------------------------------------|
| Service App domain  | `abc123.ngrok-free.app`            |
| BYoDS registration  | `https://abc123.ngrok-free.app`    |
| Gateway JWT config  | `https://abc123.ngrok-free.app`    |

### Choose Your Hosting Option

#### Option 1: Development/Testing with ngrok (Recommended)

Perfect for learning and testing BYOVA integrations.

##### Install and Configure ngrok

1. **Install ngrok**

   ```bash
   # macOS with Homebrew
   brew install ngrok/ngrok/ngrok
   
   # Or download from https://ngrok.com/download
   ```

2. **Create free account** at [ngrok.com](https://ngrok.com)
   - Sign up (free tier includes what you need)
   - Copy your authtoken from the dashboard

3. **Configure authentication**

   ```bash
   ngrok config add-authtoken YOUR_AUTHTOKEN_HERE
   ```

##### Start ngrok Tunnel

```bash
# Start tunnel to your local gateway (port 50051)
# Use HTTP/2 protocol (required for gRPC)
ngrok http --upstream-protocol=http2 50051
```

**Important**: Keep this terminal open while testing!

##### Save Your ngrok URL

ngrok displays output like:

```text
Forwarding  https://abc123def456.ngrok-free.app -> http://localhost:50051
```

**Your public URL is**: `https://abc123def456.ngrok-free.app`

**Save this URL** - you'll use it in Steps 4 and 5:

- In Step 4 (Gateway JWT config): `https://abc123def456.ngrok-free.app`
- In Step 5.2 (Service App domain): `abc123def456.ngrok-free.app` (domain only)
- In Step 5.3 (BYoDS registration): `https://abc123def456.ngrok-free.app`

**ngrok Tips**:

- Free tier URL changes each time you restart ngrok
- Monitor requests at `http://localhost:4040` (ngrok dashboard)
- Keep the terminal running - don't close it during testing

#### Option 2: Production Hosting

For production deployments, use a permanent domain with HTTPS.

**Requirements**:

- Public domain name (e.g., `byova-gateway.yourcompany.com`)
- HTTPS/TLS certificate (Let's Encrypt or commercial CA)
- Reverse proxy or load balancer routing to port 50051
- Firewall rules allowing inbound HTTPS (port 443)

**Hosting Options**:

- Cloud VM (AWS EC2, Azure VM, Google Compute Engine)
- Container platform (Kubernetes, ECS, Cloud Run)
- On-premises server with public IP

**Your URL format**: `https://byova-gateway.yourcompany.com`

**Setup Requirements**:

- Configure reverse proxy/load balancer to forward to backend port 50051
- Install valid TLS certificate
- Configure DNS A/CNAME record

### What's Next?

Now that you have your public URL, you'll use it in:

- **Step 4**: Configure gateway JWT authentication
- **Step 5**: Register with Webex Contact Center via BYODS

**Remember**: Use the same URL format everywhere - no port numbers!

---
