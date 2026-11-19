---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-virtual-agent-mtls-authentication
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Configure the gRPC server
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bring-your-own-virtual-agent-mtls-authentication). [Full Markdown](../../../../docs/bring-your-own-virtual-agent-mtls-authentication.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md)

## Article introduction

Add optional mutual TLS (mTLS) client authentication to a Bring Your Own Virtual Agent (BYOVA) gRPC endpoint while retaining the existing JWS/JWT validation.

## Selected section

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
