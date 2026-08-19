# Harvested OpenAPI (Swagger 2.0) — Availity

These files are **verbatim, first-party** API descriptions harvested from Availity's own
developer portal on 2026-08-14. They are the authoritative machine-readable contracts.

Discovery path (STEP 0b): the Availity developer portal renders its API reference
client-side with Stoplight Elements / Redoc. The public product pages embed the real
document URLs, of the form:

    https://developer.availity.com/system/api_details/<product>/oasdocument/<product>.<timestamp>.json

Source pages (both public, HTTP 200):
  - https://developer.availity.com/portal/catalogue-products/healthcare-hipaa-transactions-1
  - https://developer.availity.com/portal/catalogue-products/aws-availity-payer-list-1

Ownership check (STEP 0c): every document declares `host: api.availity.com` — the same host
carried as `baseURL` on every `apis[]` entry in apis.yml — and every document was fetched from
`developer.availity.com`, Availity's own developer portal. `securityDefinitions.oauth2.tokenUrl`
is `https://api.availity.com/v1/token`, matching the token endpoint Availity documents in its
public API Guide. Contract ownership is confirmed.

Format: Swagger 2.0 (`"swagger": "2.0"`), as published. Not converted, not modified.
