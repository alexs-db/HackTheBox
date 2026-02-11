# Well-Known URIs

The `.well-known` standard, defined in RFC 8615, serves as a standardized directory within a website's root domain. Accessible via the `/.well-known/` path, it centralizes critical metadata including configuration files and security information.

This approach enables clients to automatically locate and retrieve configuration by constructing the appropriate URL. For example: `https://example.com/.well-known/security.txt`

## Common .well-known URIs

| URI | Description | Status | Reference |
|-----|-------------|--------|-----------|
| `security.txt` | Security researcher contact information | Permanent | RFC 9116 |
| `change-password` | Standard password change page URL | Provisional | [W3C Spec](https://w3c.github.io/webappsec-change-password-url/) |
| `openid-configuration` | OpenID Connect configuration | Permanent | [OpenID Connect Discovery](http://openid.net/specs/openid-connect-discovery-1_0.html) |
| `assetlinks.json` | Digital asset ownership verification | Permanent | [Digital Asset Links](https://github.com/google/digitalassetlinks) |
| `mta-sts.txt` | SMTP MTA Strict Transport Security | Permanent | RFC 8461 |

## Web Reconnaissance with .well-known

The `openid-configuration` endpoint is particularly valuable in web recon. Accessing `https://example.com/.well-known/openid-configuration` returns OpenID Connect Provider metadata:

```json
{
    "issuer": "https://example.com",
    "authorization_endpoint": "https://example.com/oauth2/authorize",
    "token_endpoint": "https://example.com/oauth2/token",
    "userinfo_endpoint": "https://example.com/oauth2/userinfo",
    "jwks_uri": "https://example.com/oauth2/jwks",
    "response_types_supported": ["code", "token", "id_token"],
    "scopes_supported": ["openid", "profile", "email"]
}
```

### Key Reconnaissance Opportunities

- **Authorization Endpoint** — User authorization request URL
- **Token Endpoint** — Token issuance location
- **Userinfo Endpoint** — User information retrieval
- **JWKS URI** — Cryptographic keys used by the server
- **Supported Scopes & Response Types** — Functional capabilities
- **Signing Algorithms** — Security implementation details

Exploring the IANA registry provides comprehensive reconnaissance of a website's security landscape.
