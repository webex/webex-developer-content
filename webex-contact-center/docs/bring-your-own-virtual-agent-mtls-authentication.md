---
type: Guide
title: Bring Your Own Virtual Agent | mTLS Authentication
display_title: mTLS Authentication
canonical_url: https://developer.webex.com/docs/bring-your-own-virtual-agent-mtls-authentication
content_type: documentation
product_group:
- webex-contact-center
categories:
- mcp
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/bring-your-own-virtual-agent-mtls-authentication)

Add optional mutual TLS (mTLS) client authentication to a Bring Your Own Virtual Agent (BYOVA) gRPC endpoint while retaining the existing JWS/JWT validation.

## Overview

mTLS adds transport-layer authentication in both directions: Webex CCAI validates your gRPC server certificate, and your server validates the client certificate presented by Webex CCAI. The handshake completes before application data is sent.

mTLS is optional and applies only to the gRPC variant of BYOVA. It does not apply to the WebSocket variant. Enabling mTLS does not replace JWS/JWT validation; continue to validate the authorization token on every connection.

## Before you begin

Prepare the following:

- A BYOVA gRPC endpoint that already performs JWS/JWT validation.
- A publicly issued certificate and corresponding private key for the domain of your gRPC server.
- The IdenTrust Commercial Root CA 1 certificate, available from the [IdenTrust Downloads and Drivers page](https://www.identrust.com/support/downloads), which your server uses to validate the Webex CCAI client certificate.
- The Webex CCAI certificate identity and FQDNs for your tenant's environment and region. Some Webex-provided fully qualified domain names (FQDNs) must be added to your allowlist. Obtain the exact values from the Webex Contact Center documentation provided for your tenant.

The certificate Subject values and required FQDNs vary by environment and region. Do not copy or infer values from another deployment.

## Configure the gRPC server

1. Configure the server's SSL context with its publicly issued certificate and private key.
2. Add the IdenTrust root CA certificate to the trust manager that validates client certificates.
3. Set the server's client-authentication mode to `REQUIRE`. The TLS handshake must fail when the client does not present a trusted certificate.
4. Register a gRPC server interceptor that reads the peer certificate from the connection's `SSLSession` and rejects the call when the certificate is missing or invalid.
5. Validate the certificate identity against the exact Webex-provided values for the tenant's environment and region, using the certificate field specified by Webex. Also validate the issuer and certificate validity period. Separately, add the required Webex-provided FQDNs to your allowlist.
6. Keep the existing JWS/JWT authorization interceptor enabled and registered with the server.

For a Netty-based Java server, the essential SSL context configuration is:

```java
SslContext sslContext = GrpcSslContexts
        .configure(SslContextBuilder.forServer(certFile, keyFile))
        .trustManager(idenTrustRootCaFile)
        .clientAuth(ClientAuth.REQUIRE)
        .build();

Server server = NettyServerBuilder.forPort(PORT)
        .sslContext(sslContext)
        .intercept(new ClientCertificateInterceptor())
        .intercept(authorizationServerInterceptor)
        // Add the existing BYOVA services and other interceptors.
        .build()
        .start();
```

In `ClientCertificateInterceptor`, retrieve the TLS session from `Grpc.TRANSPORT_ATTR_SSL_SESSION`, require at least one peer certificate, and validate the leaf `X509Certificate` before passing the call to the next handler. Return `UNAUTHENTICATED` when the TLS session or client certificate is unavailable or the certificate identity fails validation.

See the authoritative [mTLS authentication reference implementation](https://github.com/CiscoDevNet/webex-contact-center-provider-sample-code/blob/main/mtls-authentication.md) for the complete Java interceptor pattern. You can apply it to the [BYOVA gRPC Java sample](https://github.com/CiscoDevNet/webex-contact-center-provider-sample-code/tree/main/bring-your-own/virtual-agent/grpc-interface/simulators/byova-grpc-java).

## Verify the connection

Verify all authentication layers before enabling mTLS in production:

1. Connect without a client certificate and confirm that the TLS handshake fails.
2. Connect with a certificate that is not trusted or is not in the configured identity allowlist and confirm that the connection is rejected.
3. Connect with the valid Webex CCAI certificate for the tenant's environment and region and confirm that the TLS handshake succeeds.
4. After the mTLS handshake succeeds, send a request with an invalid JWS/JWT and confirm that the authorization interceptor rejects it.
5. Send a request with both a valid client certificate and valid JWS/JWT, then confirm that the BYOVA gRPC service receives the request.

An mTLS handshake proves the transport peer's certificate identity. The JWS/JWT check separately authorizes the BYOVA request and remains required.
