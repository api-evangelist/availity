---
name: Estimate patient cost with Availity
description: >-
  Produce a pre-service patient cost estimate through Availity's predetermination APIs — professional,
  institutional and dental — including the two different Patient Cost Estimator generations (1.0.0
  synchronous-ish and 2.0.0 async pipeline) and which one to call.
api: openapi/_harvested/availity-patient-cost-estimator-professional-swagger.json
operations:
  - submitProfPredetermination
  - getProfessionalClaim
  - createProfessionalClaim
  - createInstitutionalClaim
  - getInstitutionalClaim
  - createDentalClaim
  - getDentalClaim
generated: '2026-08-15'
method: generated
source: openapi/_harvested/*-swagger.json + https://developer.availity.com/portal/catalogue-products/healthcare-hipaa-transactions-1
---

# Estimate patient cost with Availity

Base host `https://api.availity.com`. PHI throughout.

## Pick the right product first

Availity ships **three** predetermination surfaces and two generations of the professional one.
They are separate APIs with separate base paths, not versions of one endpoint:

| Product | Base path | Create | Poll |
|---|---|---|---|
| Patient Cost Estimator 1.0.0 — Professional | `/v1` | `POST /professional-claims` (`createProfessionalClaim`) | `GET /professional-claims/{id}` (`getProfessionalClaim`) |
| Patient Cost Estimator 1.0.0 — Institutional | `/v1` | `POST /institutional-claims` (`createInstitutionalClaim`) | `GET /institutional-claims/{id}` (`getInstitutionalClaim`) |
| Patient Cost Estimator 2.0.0 — Professional | `/v2/patient-cost-estimates/prof` | `POST /` (`submitProfPredetermination`) | `GET /{id}` (`getProfessionalClaim`) |
| Dental Claims | `/v1` | `POST /dental-claims` (`createDentalClaim`) | `GET /dental-claims/{id}` (`getDentalClaim`) |

Two things to note:

1. **`getProfessionalClaim` is used as the operationId in BOTH the 1.0.0 and the 2.0.0 professional
   documents, on different base paths.** If you generate clients from both specs into one namespace
   you will get a collision. Namespace by product.
2. Availity's breaking-change practice is to ship a **new product with a new base path** rather than
   mutate an existing version — 2.0.0 - Professional did not replace 1.0.0 - Professional, it sits
   beside it. There is no deprecation policy and no Sunset header telling you when the older one
   goes away. See `lifecycle/availity-lifecycle.yml`.

Choose 2.0.0 for new professional work: it is the async pipeline with the richer response
(`ProfessionalPCEResponse`, `PollingResponse`, `CoveragePlanCandidates`).

## 1. Token

`POST /v1/token`, form-encoded, `grant_type=client_credentials` + credentials +
`scope=healthcare-hipaa-transactions <plan-scope>`. 300 seconds, no refresh, case sensitive.

## 2. Submit — `submitProfPredetermination` (2.0.0)

`POST /v2/patient-cost-estimates/prof`

Declared responses: `202`, `400`, `401`, `403`, **`422`**, `500`.

`422 Unprocessable Entity` is declared on this API and not on most of the others — it is where a
payer-side rejection of the predetermination surfaces. Read `errors[].errorMessage` for the specific
field and fix it; do not retry unchanged.

Success is `202 Accepted`. Persist the id from `Location`.

## 3. Poll — `getProfessionalClaim` (2.0.0)

`GET /v2/patient-cost-estimates/prof/{id}`

Declared responses: `200`, `202`, `400`, `401`, `403`, `404`, `422`, `500`, **`502`**, **`503`**, **`504`**.

This is the widest failure surface in Availity's estate and it tells you exactly where the failure
is:

- `202` — still running. Poll again. **Not** success.
- `200` — the estimate is ready.
- `502` — failure between Availity and the payer. Re-poll.
- `503` — payer connectivity down or in a maintenance window. Back off; `getCustomPayerList` reports per-payer transaction availability.
- `504` — the payer response timed out. **Re-poll the same id. Do NOT re-submit.** There is no idempotency key on this API, so re-submitting risks a duplicate predetermination.

## 4. The 1.0.0 and dental flows

Identical shape: `POST` returns `202`, `GET /{id}` returns `202` while pending and `200` when ready,
with `504` declared on the GET for a payer timeout. Same rule — re-poll, never re-submit.

## 5. Response shapes

2.0.0 professional: `ProfessionalPCERequest` / `ProfessionalPCEResponse`, `PollingResponse`,
`CoveragePlanCandidates`, `ProfessionalClaimBase` (which `has_one Subscriber`, and
`Subscriber has_many ItemDescription` via `holdReasons` — read `holdReasons` to find out why an
estimate is held).

1.0.0 professional: `ProfessionalClaim` -> `Subscriber`, plus `ClaimAdjustmentGroup`,
`AmbulanceCertification`, `PhysicalLocation`, `Provider`, `SupplementalInformation`.

Institutional: `InstitutionalClaim` with `Diagnosis`, `Procedure`, `ItemDescription`.

Dental is the widest structure in the estate:

```
DentalClaim
  billingProvider  -> BillingProvider
  patient          -> Patient
  payer            -> Payer
  submitter        -> Submitter
  subscriber       -> Subscriber
  claimInformation -> ClaimInformation
                        diagnoses[]  -> Diagnosis
                        serviceLines[] -> ServiceLine
                        otherPayers[]  -> OtherPayer
                        toothStatuses[] -> ToothStatus
                        notes[]        -> Note
                        + six provider roles: renderingProvider, referringProvider,
                          supervisingProvider, assistantSurgeon, primaryCareProvider,
                          serviceFacility (each -> Provider)
```

`ServiceLine` repeats four of those provider roles at line level and carries
`adjudicationInformation[]` -> `AdjudicationInformation` -> `claimAdjustmentGroups[]` ->
`AdjustmentGroup` -> `adjustments[]` -> `Adjustment`. That four-level chain is where the money
actually is — the estimate's adjustments live there, not on the claim root.

Entity graph: `data-model/availity-data-model.yml`.

## Errors

Custom envelope, not RFC 9457. Note that on the 2.0.0 professional document `ErrorResponse` is
declared with `candidates[] -> CoveragePlanCandidates` rather than the usual
`errors[] -> FieldError` — this API's error body carries coverage-plan candidates when it cannot
determine which plan to price against. Handle it as a product-specific shape.

Full catalogue: `errors/availity-problem-types.yml`.

## Testing

Demo plan scope, `X-Api-Mock-Scenario-ID`, assert `X-Api-Mock-Response: true`. Remember the Demo
environment returns canned data, so it cannot validate payer-specific pricing rules. See
`sandbox/availity-sandbox.yml`.
