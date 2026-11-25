---
type: Excerpt
canonical_url: https://developer.webex.com/docs/byova-and-aws-lex
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Troubleshooting
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/byova-and-aws-lex). [Full Markdown](../../../../docs/byova-and-aws-lex.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](002-prerequisites.md)

## Article introduction

Transform your contact center with intelligent voice interactions using Webex Contact Center's BYOVA (Bring Your Own Virtual Agent) feature and AWS Lex.

## Selected section

## Troubleshooting

### Common Issues and Solutions

### Gateway Startup Issues

#### Problem: Gateway fails to start - "datasource_url not configured"

**Cause**: JWT validation enabled but no datasource URL set

**Solution**:

1. Verify Step 3 is complete (you have a public URL)
2. Edit `config/config.yaml`:

   ```yaml
   jwt_validation:
     enabled: true
     datasource_url: "https://your-public-url"  # No port!
   ```

3. Or temporarily disable for testing:

   ```yaml
   jwt_validation:
     enabled: false
   ```

#### Problem: Gateway fails to start - dependency errors

**Solution**:

```bash
# Ensure virtual environment is activated
source venv/bin/activate

# Reinstall dependencies
pip install -r requirements.txt
```

#### 1. Gateway Won't Start

**Problem**: `python: command not found` or import errors

**Solution**: Ensure virtual environment is activated

```bash
source venv/bin/activate
which python  # Should show venv path
```

### JWT Authentication Issues

#### Problem: "JWT validation failed: datasource URL mismatch"

**Cause**: URL in gateway config doesn't match BYoDS registration

**Solution**:

1. Check your BYoDS datasource registration (Step 5.3)
2. Copy the EXACT URL you registered (including `https://`, no port)
3. Update `config/config.yaml` to match:

   ```yaml
   jwt_validation:
     datasource_url: "https://abc123.ngrok-free.app"  # Must match BYoDS exactly
   ```

4. Restart gateway

**Debug command**:

```bash
# View your registered datasource
curl -H "Authorization: Bearer YOUR_TOKEN" \
  https://webexapis.com/v1/datasources/YOUR_DATASOURCE_ID
```

#### Problem: "Invalid issuer" in JWT logs

**Cause**: JWT from unsupported or malformed issuer

**Solution**:

1. Verify BYOVA is enabled for your org (Step 1.4)
2. Check datasource configuration in WxCC Control Hub
3. Supported issuers:
   - `https://idbrokerbts.webex.com/idb` (BTS US)
   - `https://idbrokerbts-eu.webex.com/idb` (BTS EU)
   - `https://idbroker.webex.com/idb` (Production US)
   - `https://idbroker-eu.webex.com/idb` (Production EU)
   - `https://idbroker-b-us.webex.com/idb` (B-US)
   - `https://idbroker-ca.webex.com/idb` (Canada)

**Additional Resources**:

- [JWT Implementation Summary](../../../../docs/JWT_IMPLEMENTATION_SUMMARY.md)
- [Authentication Quick Start](../../../../docs/AUTHENTICATION_QUICKSTART.md)

### URL Configuration Issues

#### Problem: Service App registration fails

**Solution**: Verify domain format

- ✅ Correct: `abc123.ngrok-free.app`
- ❌ Wrong: `https://abc123.ngrok-free.app`
- ❌ Wrong: `abc123.ngrok-free.app:50051`

#### Problem: Webex can't reach gateway

**Solution**:

1. Verify ngrok is running: `curl http://localhost:4040/api/tunnels`
2. Check gateway is listening: `curl http://localhost:8080/health`
3. Test public URL: `curl https://your-ngrok-url/health`
4. Verify URL matches in:
   - BYoDS registration (Step 5.3)
   - Gateway JWT config (Step 4.2)

#### 2. AWS Lex Connection Issues

**Problem**: Authentication or region errors
**Solution**: Verify AWS credentials and region
```bash
aws sts get-caller-identity  # Test AWS credentials
```

#### 3. Webex Contact Center Can't Reach Gateway
**Problem**: Connection timeout or refused

**Solution**: Check network configuration

- Verify gateway IP address
- Ensure port 50051 is accessible
- Check firewall settings

#### 4. Audio Quality Issues

**Problem**: Poor audio quality or delays

**Solution**: Check audio configuration

- Verify sample rate (8000 Hz)
- Check encoding (u-law)
- Review network latency

#### 5. Bot Not Responding

**Problem**: Lex bot doesn't respond to utterances

**Solution**: Check bot configuration

- Verify bot alias ID
- Test bot in Lex console
- Check intent configuration

### Debug Commands

```bash
# Check gateway status
curl http://localhost:8080/api/status

# View active connections
curl http://localhost:8080/api/connections

# Check debug information
curl http://localhost:8080/api/debug/sessions

# Test AWS credentials
aws sts get-caller-identity

# Check Lex bot status
aws lex-models-v2 describe-bot --bot-id YOUR_BOT_ID
```

---
