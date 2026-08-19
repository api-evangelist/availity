---
name: Check claim status with Availity
description: >-
  Run an X12 276/277 claim status inquiry through the Availity clearinghouse — submit the request,
  poll correctly through the 202 accept-then-poll cycle, and read the per-claim, per-service-line
  status detail out of the response.
api: openapi/_harvested/availity-claim-statuses-swagger.json
operations:
  - getCustomPayerList
  - findClaimStatus
  - getClaimStatusById
generated: '2026-08-15'
method: generated
source: openapi/_harvested/availity-claim-statuses-swagger.json + https://developer.availity.com/blog/2025/3/25/availity-api-guide
---

# Check claim status with Availity

Base host `https://api.availity.com`. PHI throughout.

## 1. Token

`POST /v1/token` with `grant_type=client_credentials`, `client_id`, `client_secret` and
`scope=healthcare-hipaa-transactions <plan-scope>`. 300-second lifetime, no refresh token, case
sensitive parameters. Send `Authorization: Bearer <token>`.

## 2. Confirm the payer supports 276/277 — `getCustomPayerList`

`GET /v1/availity-payer-list`. Not every payer on the Availity network accepts a claim status
inquiry. Check the payer's supported transaction list first.

## 3. Submit the inquiry — `findClaimStatus`

`POST /v1/claim-statuses`

This is the X12 276. It is a **POST that performs a query** — Availity models the inquiry as a
created resource, so do not look for a GET-with-query-parameters form.

Declared responses: `200`, `202`, `400`, `401`, `403`, `500`.

- `200` — the payer answered inline.
- `202` — accepted, still processing. Take the `Location` header and poll.

## 4. Poll — `getClaimStatusById`

`GET /v1/claim-statuses/{id}`

Declared responses: `200`, `202`, `400`, `401`, `403`, `404`, `500`.

**This is the single most important rule for Availity.** `202` is returned on the GET as well as on
the POST. On the GET it means *not finished — poll again*. An agent that treats `202` as success
will report "no claims found" on a request that is still in flight. Only `200` carries the payer's
X12 277 response.

Poll with backoff. There is no webhook, no callback and no event stream — polling is the only
completion mechanism Availity offers.

## 5. Read the result

```
ClaimStatus
  patient        -> Patient
  subscriber     -> Subscriber
  payer          -> Payer
  submitter      -> Submitter       (submitter.statusDetails[] -> ClaimStatusDetail)
  providers[]    -> Provider        (provider.statusDetails[]  -> ClaimStatusDetail)
  claimStatuses[]-> ClaimStatusResult
                      statusDetails[] -> ClaimStatusDetail
                      serviceLines[]  -> ServiceLine
                                           statusDetails[] -> ClaimStatusDetail
```

`ClaimStatusDetail` appears at **four** levels — submitter, provider, claim and service line. A
rejection at submitter or provider level means the inquiry never reached claim matching, and the
claim-level array will be empty. Check the outer levels before concluding the claim does not exist.

A paged inquiry returns `ResultSet` with a `claimStatuses` array of `ClaimStatusSummary` (the
summary shape, not the full `ClaimStatusResult`); fetch the id to get detail.

Entity graph: `data-model/availity-data-model.yml`.

## Deleting

`DELETE /v1/claim-statuses/{id}` exists in Availity's document but is published **with no
operationId, no summary and no description**. It is not part of this skill because there is no
documented contract for it. Do not call it from generated code.

## Errors

Custom envelope `{statusCode, reasonCode, userMessage, developerMessage, url, errors[]}` served as
`application/json` — not RFC 9457.

- `401` — expired token far more often than bad credentials (300-second lifetime).
- `403` — not subscribed/entitled to the product or plan.
- `429` — no rate-limit headers and no `Retry-After`; back off blind. Standard plan: 100 calls/sec, 100,000 calls/day.
- `500` — retry with backoff, quote `X-Availity-Transaction-ID` on the support ticket.

Full catalogue: `errors/availity-problem-types.yml`.

## Testing

Demo plan scope + `X-Api-Mock-Scenario-ID`, and assert `X-Api-Mock-Response: true` on every
response. See `sandbox/availity-sandbox.yml`.
