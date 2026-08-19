---
name: Authenticate against the Availity APIs
description: >-
  Obtain and manage an Availity OAuth 2.0 client-credentials token — the scope vocabulary that
  selects product, plan and sandbox-vs-production, the 300-second lifetime, and the failure modes a
  long-running agent will hit.
api: openapi/_harvested/availity-coverages-swagger.json
operations:
  - createCoverage
  - getCustomPayerList
generated: '2026-08-15'
method: generated
source: https://developer.availity.com/blog/2025/3/25/availity-api-guide + openapi/_harvested/*-swagger.json (securityDefinitions.oauth2)
---

# Authenticate against the Availity APIs

Availity supports exactly one authentication method on its public REST APIs: the OAuth 2.0 **Client
Credentials Grant**, application-only. There is no user identity layer, no OIDC, no API key header,
no mTLS.

## The token request

```
POST https://api.availity.com/v1/token
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials
client_id=<your client id>
client_secret=<your client secret>
scope=<product-scope> <plan-scope>
```

Availity explicitly warns that **the body parameter names and values are case sensitive**. A
lowercase/uppercase mismatch fails as a credential error rather than a validation error, which is a
common wasted afternoon.

Response:

```json
{"access_token":"...","token_type":"Bearer","expires_in":300,"scope":"...","consented_on":...}
```

Use it as `Authorization: Bearer <access_token>` over HTTPS. HTTP is not supported — every Availity
document declares `schemes: [https]` only.

## Scopes are not permissions

This is the part that surprises people. Availity's OAuth scopes are **not** read/write verbs and
there is **no per-operation scoping**. They are identifiers: one names the API PRODUCT you
subscribed to, the second names the PLAN tier within it. Send both, space-separated.

```
scope=healthcare-hipaa-transactions healthcare-hipaa-transactions-demo
scope=healthcare-hipaa-transactions healthcare-hipaa-transactions-standard
```

Known product scopes: `healthcare-hipaa-transactions`,
`healthcare-hipaa-transactions-highvolume`, `rcm-coverages`, `aws-availity-payer-list`. Plan scopes
suffix the product with `-demo`, `-standard`, or `-unlimited`. Full vocabulary:
`scopes/availity-scopes.yml`.

**The plan scope is what selects sandbox versus production.** Same host, same token format, same
code path. Getting it wrong means transacting live PHI. Assert `X-Api-Mock-Response: true` on
responses in any non-production run.

### The `hipaa` scope trap

Every Availity Swagger document declares its operation-level requirement as
`security: [{"oauth2": ["hipaa"]}]` — referencing a scope named `hipaa` that is **not defined** in
any `securityDefinitions.scopes` map and that Availity's token endpoint will not grant. It appears
to be a stale literal in the gateway's spec-generation template. A code generator reading these
specs will emit a token request for `scope=hipaa` and it will not work. Override it with the
product/plan pair above.

## The 300-second lifetime

`expires_in` is **300** — five minutes — and Availity issues **no refresh token**. You re-run the
grant.

Consequences for anything long-running:

- Any batch job or agent loop running longer than five minutes must re-authenticate mid-run.
- **Interpret a mid-session `401` as an expired token before you interpret it as a bad credential.** This is the single most common false alarm against Availity.
- Do **not** fetch a token per request. Token acquisition is not documented as exempt from the rate limit, so a naive per-call grant burns plan quota against the 100 calls/second / 100,000 calls/day Standard ceiling.
- Cache the token, refresh at roughly 80% of its life (~240 seconds), and serialize refreshes so a burst of concurrent calls does not stampede the token endpoint.

## No discovery document

There is no `/.well-known/oauth-authorization-server` and no `/.well-known/openid-configuration` on
any Availity host — `developer.availity.com` and `www.availity.com` return their site catch-all HTML
for those paths and `api.availity.com` returns `401` for every path. The token endpoint is
discoverable only from prose documentation and from `securityDefinitions.oauth2.tokenUrl` inside each
Swagger document. Hard-code it: `https://api.availity.com/v1/token`.

## Getting credentials

1. Create a `developer.availity.com` account — email verification plus **mandatory MFA** via an authenticator app.
2. Create an Organization. Adding other users to it requires a support ticket with case reason "API".
3. Register an application under **My Apps** to get the client id and client secret.
4. Subscribe the application to a product and plan. **Demo is auto-approved and free.**
5. Standard/production requires a portal request **and** a sales conversation; Trading Partner Management completes contracting before activation. Budget for a contract, not a signup.

## Related headers

- `X-Availity-Customer-Id` (request) — identifies the customer organization you are acting for.
- `X-Availity-Transaction-ID` (response) — quote it on every support ticket.
- `X-Response-Encoding-Context` (request) — contextual output encoding is **opt-in**. Availity does not escape response data by default and the payload is PHI destined for clinical UIs. Send this header or escape it yourself.

Profile: `authentication/availity-authentication.yml`.
