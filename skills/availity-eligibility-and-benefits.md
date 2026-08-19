---
name: Verify patient eligibility and benefits with Availity
description: >-
  Run a real-time X12 270/271 eligibility and benefits check through the Availity clearinghouse —
  confirm the payer supports the transaction, fetch that payer's field requirements, submit the
  coverage request, then read co-pay, deductible and out-of-pocket amounts out of the benefits graph.
api: openapi/_harvested/availity-coverages-swagger.json
operations:
  - getCustomPayerList
  - findConfigurations
  - createCoverage
  - getCoverageById
  - deleteCoverageById
generated: '2026-08-15'
method: generated
source: openapi/_harvested/*-swagger.json + https://developer.availity.com/blog/2025/3/25/availity-api-guide
---

# Verify patient eligibility and benefits with Availity

Base host `https://api.availity.com`. Everything here is PHI. Do not run it outside a Demo
subscription unless a signed trading-partner agreement and a BAA are in place.

## 1. Get a token

`POST https://api.availity.com/v1/token`, `application/x-www-form-urlencoded`:

```
grant_type=client_credentials
client_id=<your client id>
client_secret=<your client secret>
scope=healthcare-hipaa-transactions healthcare-hipaa-transactions-demo
```

Parameter names and values are **case sensitive**. The token lives **300 seconds** and there is no
refresh token — re-run the grant. Send it as `Authorization: Bearer <access_token>` on every call.

Swap the second scope for `healthcare-hipaa-transactions-standard` only when you intend to
transact against live payers.

## 2. Confirm the payer supports 270/271 — `getCustomPayerList`

`GET /v1/availity-payer-list`

Returns the payers available under your contract and which transactions each supports. Filter for
the payer you need and confirm eligibility is in its supported transaction list before submitting.
Skipping this is the usual cause of an otherwise unexplainable rejection.

Paginate with `offset` (min 0, default 0) and `limit` (min 1, **max 50**, default 50). The response
array is named `payers` — the plural resource name, not `data` or `results`.

## 3. Fetch that payer's field requirements — `findConfigurations`

`GET /v1/configurations`

Query by type, sub-type and payer. This returns the payer-specific validation rules and required
fields. Availity's Demo environment returns **canned** responses and will not enforce these, so a
request that passes in Demo can still be rejected in production. Read the configuration first and
validate locally.

## 4. Submit the eligibility request — `createCoverage`

`POST /v1/coverages`

This is the X12 270. Note that Availity's own document declares this operation with `formData`
parameters, so it is form-encoded rather than a JSON request body — a `415 Unsupported Media Type`
here almost always means a JSON body was sent.

Responses: `200`, `202`, `400`, `401`, `403`, `500`.

- `200` — the payer answered synchronously; the coverage is in the body.
- `202` — accepted, still processing. Read the `Location` header and poll step 5.

## 5. Poll for the benefits response — `getCoverageById`

`GET /v1/coverages/{id}`

Responses: `200`, `401`, `403`, `404`, `500`.

**There is no idempotency key on this API.** If a submit times out, do **not** re-submit — poll the
id you were given. Re-submitting a coverage request is comparatively cheap, but the same habit
applied to a claim or a service review causes duplicate adjudication, so build the poll-don't-resubmit
reflex here.

## 6. Read the benefits graph correctly

This is where most integrations get it wrong. The structure is four levels deep:

```
Coverage
  payer            -> Payer
  requestingProvider -> HealthCareContact
  benefits[]       -> Benefit
                        amounts -> Amounts
                                     coPayment    -> BenefitDetail
                                     coInsurance  -> BenefitDetail
                                     deductibles  -> BenefitDetail
                                     outOfPocket  -> BenefitDetail
                                                       inNetwork[]            -> NetworkBenefit
                                                       outOfNetwork[]         -> NetworkBenefit
                                                       noNetwork[]            -> NetworkBenefit
                                                       notApplicableNetwork[] -> NetworkBenefit
```

`BenefitDetail` fans out into **four** network buckets. Reading only `inNetwork` will silently drop
the out-of-network deductible and misquote the patient. Walk all four.

`Benefit` also carries `limitations`, `exclusions`, `nonCovered`, `preexistingConditions` and
`costContainment`, each a `BenefitDetail`. A benefit that looks covered in `amounts` can be
excluded in `nonCovered`. Check both before telling a patient they are covered.

Full entity graph: `data-model/availity-data-model.yml`.

## 7. Clean up if required — `deleteCoverageById`

`DELETE /v1/coverages/{id}` (`204` on success). Availity stores the coverage response; delete it
when your retention policy requires it.

## Errors

Availity returns a custom envelope, **not** RFC 9457 problem+json:

```json
{"statusCode":404,"reasonCode":0,"userMessage":"...","developerMessage":"...","url":"...","errors":[{"code":0,"errorMessage":"..."}]}
```

- `400` — malformed request, or Availity's allow-list input validation rejected a character (look for "inbound injection" in `developerMessage`).
- `401` — almost always an **expired token**, not a bad credential. Tokens last 300 seconds.
- `403` — the application is authenticated but not subscribed/entitled to this product or plan.
- `422` — payer-side rejection. Read `errors[].errorMessage` and fix the X12 field.
- `429` — rate limit. There are **no** `X-RateLimit-*` / `RateLimit-*` headers and no `Retry-After`; back off exponentially with jitter against the published ceiling (100 calls/sec, 100,000 calls/day on Standard).

Quote the `X-Availity-Transaction-ID` response header on any support ticket.

Full catalogue: `errors/availity-problem-types.yml`.

## Testing

Subscribe on the Demo plan and request the `-demo` scope. Send `X-Api-Mock-Scenario-ID` to select a
canned scenario, and **assert `X-Api-Mock-Response: true` on every response** — the host and token
format are identical in Demo and production, so that header is the only runtime proof you are not
touching live PHI. See `sandbox/availity-sandbox.yml`.
