---
name: Submit and track a prior authorization with Availity
description: >-
  Run an X12 278 service review through the Availity clearinghouse — check the payer's requirements,
  create the authorization request, poll for the payer's decision, and update or void it. Includes
  the duplicate-submission hazard created by Availity shipping no idempotency key.
api: openapi/_harvested/availity-service-reviews-swagger.json
operations:
  - getCustomPayerList
  - findConfigurations
  - createServiceReview
  - getServiceReviewById
  - findServiceReviews
  - updateServiceReview
  - voidServiceReview
generated: '2026-08-15'
method: generated
source: openapi/_harvested/availity-service-reviews-swagger.json + https://developer.availity.com/blog/2025/3/25/availity-api-guide
---

# Submit and track a prior authorization with Availity

Base host `https://api.availity.com`. Service Reviews is on **`/v2`**, not `/v1`. PHI throughout.

## 1. Token

`POST /v1/token`, form-encoded, `grant_type=client_credentials` + `client_id` + `client_secret` +
`scope=healthcare-hipaa-transactions <plan-scope>`. 300 seconds, no refresh. Case sensitive.

## 2. Confirm the payer accepts 278 — `getCustomPayerList`

`GET /v1/availity-payer-list`. Prior authorization support varies more by payer than any other
transaction on the network. Check before submitting.

## 3. Fetch the payer's requirements — `findConfigurations`

`GET /v1/configurations`

Query by type, sub-type and payer for the prior-authorization configuration. This is where the
payer's required fields, code sets and conditional rules live. Availity's Demo environment will
**not** enforce them (responses are canned), so validate against the configuration locally before
going live.

## 4. Create the service review — `createServiceReview`

`POST /v2/service-reviews`

This is the X12 278 request. Declared responses: `202`, `400`, `401`, `403`, `500`.

Note there is **no `200` and no `201`** — a successful submission is always `202 Accepted`. Take the
`Location` header.

### Duplicate hazard — read before writing retry logic

Availity publishes **no idempotency-key header**. There is no request-replay contract. If your HTTP
client retries a `POST /v2/service-reviews` after a timeout, the payer can receive two authorization
requests for the same service. Availity pushes de-duplication onto the payer-assigned identifiers
inside the X12 payload.

Rules:

- Retry a **connection failure before the request was sent** — that is safe.
- Never retry after a `5xx` or a timeout on the POST. Poll instead: `findServiceReviews` to look for
  a review matching your patient/provider/service before creating a second one.
- Persist the id from the `Location` header before doing anything else.

## 5. Poll for the decision — `getServiceReviewById`

`GET /v2/service-reviews/{id}`

Declared responses: `200`, `202`, `400`, `401`, `403`, `404`, `500`.

`202` on this GET means **still pending at the payer**, not success. Only `200` carries the X12 278
response with the authorization decision. Poll with backoff; there is no callback.

## 6. Search existing reviews — `findServiceReviews`

`GET /v2/service-reviews`

Use this to find a review you may have already created (see the duplicate hazard above) and to page
history. Paging is `offset` / `limit` (max 50); the response is a `ResultSet` whose array is named
`serviceReviews`.

## 7. Update or void

- `PUT /v2/service-reviews` — `updateServiceReview`. Responses `202`, `400`, `401`, `403`, `500`. Again async: `202` then poll.
- `DELETE /v2/service-reviews/{id}` — `voidServiceReview`. Responses `202`, `204`, `400`, `401`, `403`, `404`, `500`. `204` is a completed void; `202` means the void itself is being processed at the payer, so poll the id.

## 8. Attach clinical documentation

Supporting documentation is carried on `ServiceReview.supplementalInformation` (which itself holds
`diagnoses[]` and `procedures[]`). Files stored by Availity are retrieved through the Dfs API,
`GET /sdk/v1/dfs/{id}` (`download`), using an encrypted URL — note that Dfs is on the `/sdk/v1` base
path, not `/v1`.

## 9. The response shape

```
ServiceReview
  patient            -> Patient
  subscriber         -> Subscriber
  payer              -> Payer
  requestingProvider -> RequestingProvider
  renderingProviders[] -> RenderingProvider
  diagnoses[]        -> Diagnosis
  procedures[]       -> Procedures     (procedures.notes[] -> Note)
  payerNotes[]       -> Note
  providerNotes[]    -> Note
  transportLocations[] -> TransportLocation
  supplementalInformation -> SupplementalInformation
  validationMessages[] -> FieldError
```

`validationMessages[]` carries `FieldError` objects on an otherwise-successful response — a `200`
can still contain field-level problems the payer flagged. Check it even on success.

Entity graph: `data-model/availity-data-model.yml`.

## Errors

Custom envelope, not RFC 9457. `401` = expired 300-second token. `403` = entitlement. `429` = rate
limit with **no** headers and no `Retry-After`. Full catalogue: `errors/availity-problem-types.yml`.

## Testing

Demo plan scope, `X-Api-Mock-Scenario-ID` to pick a scenario, and assert `X-Api-Mock-Response: true`
on every response. See `sandbox/availity-sandbox.yml`.
