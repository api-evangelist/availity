# Availity (availity)
Availity is a healthcare information network and clearinghouse providing REST APIs for real-time HIPAA EDI transactions. The platform processes over 11 billion annual healthcare transactions connecting providers, health plans, and vendors nationwide. Create your application and subscribe to a plan to make use of Availity APIs for eligibility verification, claims management, prior authorization, and patient cost estimation.

**URL:** [https://developer.availity.com/](https://developer.availity.com/)

**Run:** [Capabilities Using Naftiko](https://github.com/naftiko/fleet?utm_source=api-evangelist&utm_medium=readme&utm_campaign=company-api-evangelist&utm_content=repo)

## Tags

 - Attachments, Benefits, Care Reminders, Claims, Clearinghouse, Configuration, Cost Estimation, EDI, Eligibility, Healthcare, HIPAA, Member ID Card, Patient Financial Responsibility, Payer Network, Payer Requirements, Price Transparency, Prior Authorization, Provider Validation, Reference Data, Service Reviews, X12 270/271, X12 276/277, X12 278

## Timestamps

- **Created:** 2026-03-18
- **Modified:** 2026-04-19

## APIs

### Availity Eligibility & Benefits API
The Availity Eligibility & Benefits API supports the ASC X12N 270 and 271 transactions, enabling real-time verification of member coverage, co-pays, deductibles, and benefits information. REST APIs connect provider systems to every major health plan nationwide for eligibility checks.

**Human URL:** [https://developer.availity.com/](https://developer.availity.com/)

#### Tags

 - Benefits, EDI, Eligibility, Healthcare, X12 270/271

#### Properties

- [Documentation](https://developer.availity.com/partner/documentation)
- [GettingStarted](https://developer.availity.com/partner/gettingstarted)
- [Documentation](https://developer.availity.com/blog/2025/3/4/ebvalue-add-api)
- [OpenAPI](openapi/availity-eligibility-openapi.yml)
- [JSONSchema](json-schema/availity-eligibility-schema.json)

### Availity Claim Status API
The Availity Claim Status API enables the standard ASC X12N 276 and 277 transactions, allowing providers to find, create, and manage claim status inquiries against payer systems. REST APIs bridge provider billing systems and payers through the Availity clearinghouse network. Supports both standard 276/277 workflows and enhanced claim status with summary and detail search.

**Human URL:** [https://developer.availity.com/](https://developer.availity.com/)

#### Tags

 - Claims, Clearinghouse, EDI, Healthcare, X12 276/277

#### Properties

- [Documentation](https://developer.availity.com/partner/documentation)
- [Documentation](https://developer.availity.com/blog/2025/3/25/enhanced-claim-status)
- [GettingStarted](https://developer.availity.com/partner/gettingstarted)
- [OpenAPI](openapi/availity-claim-status-openapi.yml)

### Availity Claim Attachments API
The Availity Claim Attachments API enables electronic submission of supporting documentation alongside healthcare claims. REST APIs support structured and unstructured attachment types for additional clinical information required by payers during claims adjudication.

**Human URL:** [https://developer.availity.com/](https://developer.availity.com/)

#### Tags

 - Attachments, Claims, Clearinghouse, EDI, Healthcare

#### Properties

- [Documentation](https://developer.availity.com/blog/2025/2/28/claim-attachment-api)
- [GettingStarted](https://developer.availity.com/partner/gettingstarted)
- [OpenAPI](openapi/availity-claim-attachments-openapi.yml)

### Availity Service Reviews (Prior Authorization) API
The Availity Service Reviews API enables the ASC X12N 278 transaction for prior authorization and healthcare service review. REST APIs allow providers to find, create, and manage authorization requests and responses with health plan payers through the Availity clearinghouse. Includes IsAuthRequired and Attachments add-on APIs.

**Human URL:** [https://developer.availity.com/](https://developer.availity.com/)

#### Tags

 - EDI, Healthcare, Prior Authorization, Service Reviews, X12 278

#### Properties

- [Documentation](https://developer.availity.com/blog/2025/3/4/service-reviews)
- [GettingStarted](https://developer.availity.com/partner/gettingstarted)
- [OpenAPI](openapi/availity-service-reviews-openapi.yml)

### Availity Healthcare HIPAA Transactions API
The Availity Healthcare HIPAA Transactions API provides a unified interface for standard HIPAA EDI transactions. REST APIs enable healthcare providers and vendors to submit and receive X12 EDI transactions across payers including eligibility, claims, remittance, authorizations, and referrals. Quota: 100,000 calls per day, 100 calls per second rate limit.

**Human URL:** [https://developer.availity.com/portal/catalogue-products/healthcare-hipaa-transactions-1](https://developer.availity.com/portal/catalogue-products/healthcare-hipaa-transactions-1)

#### Tags

 - Clearinghouse, EDI, Healthcare, HIPAA

#### Properties

- [Documentation](https://developer.availity.com/portal/catalogue-products/healthcare-hipaa-transactions-1)
- [Documentation](https://developer.availity.com/blog/2025/3/25/hipaa-transactions)
- [GettingStarted](https://developer.availity.com/partner/gettingstarted)

### Availity Patient Cost Estimator API
The Availity Patient Cost Estimator API enables healthcare providers and institutions to estimate service costs before delivery for both institutional and professional services. REST APIs support version 1.0.0 and 2.0.0 and include predetermination requests across all major health plan payers, helping meet price transparency requirements.

**Human URL:** [https://developer.availity.com/](https://developer.availity.com/)

#### Tags

 - Cost Estimation, Healthcare, Patient Financial Responsibility, Price Transparency

#### Properties

- [Documentation](https://developer.availity.com/partner/documentation)
- [GettingStarted](https://developer.availity.com/partner/gettingstarted)

### Availity Eligibility & Benefits Value-Add APIs
The Availity Eligibility & Benefits Value-Add APIs provide supplementary data during eligibility transactions. The Care Reminders API retrieves real-time care gap information from multiple payers. The Member ID Card API retrieves digital member ID cards in PDF or PNG format during eligibility verification workflows.

**Human URL:** [https://developer.availity.com/](https://developer.availity.com/)

#### Tags

 - Care Reminders, EDI, Eligibility, Healthcare, Member ID Card

#### Properties

- [Documentation](https://developer.availity.com/blog/2025/3/4/ebvalue-add-api)
- [GettingStarted](https://developer.availity.com/partner/gettingstarted)

### Availity Payer List API
The Availity Payer List API (v1.0.4) allows healthcare organizations to query available payers and the transactions they support. Returns payer identifiers, names, and supported transaction types including eligibility, claim status, prior authorization, and remittance across the nationwide Availity clearinghouse network.

**Human URL:** [https://developer.availity.com/](https://developer.availity.com/)

#### Tags

 - Clearinghouse, Healthcare, Payer Network, Reference Data

#### Properties

- [Documentation](https://developer.availity.com/partner/documentation)
- [GettingStarted](https://developer.availity.com/partner/gettingstarted)

### Availity Configurations API
The Availity Configurations API (v1.0.0) provides provider details and payer-specific validation requirements. Returns configuration rules for enhanced claim status, prior authorization, and other transaction types so provider systems can validate submissions before sending to payers.

**Human URL:** [https://developer.availity.com/](https://developer.availity.com/)

#### Tags

 - Configuration, Healthcare, Payer Requirements, Provider Validation

#### Properties

- [Documentation](https://developer.availity.com/partner/documentation)
- [GettingStarted](https://developer.availity.com/partner/gettingstarted)

## Common Properties

- [Website](https://www.availity.com)
- [Portal](https://developer.availity.com/)
- [Documentation](https://developer.availity.com/partner/documentation)
- [GettingStarted](https://developer.availity.com/partner/gettingstarted)
- [Documentation](https://developer.availity.com/blog/2025/3/25/availity-api-guide)
- [Support](https://developer.availity.com/partner/contact-us)
- [TermsOfService](https://www.availity.com/terms-of-use/)
- [PrivacyPolicy](https://www.availity.com/Privacy-Policy/)
- [GitHubOrganization](https://github.com/availity)
- [SDK](https://availity.github.io/sdk-js/)

## Features

| Name | Description |
|------|-------------|
| OAuth 2.0 Authentication | Client credentials grant flow with 5-minute token expiration and HTTPS/TLS encryption for secure API access. |
| Real-Time EDI Transactions | Processing over 8.8 million daily transactions and 11 billion annual healthcare transactions across all major health plans. |
| Nationwide Payer Network | Access to every major health plan nationwide and over 1 million providers through the Availity clearinghouse. |
| Multi-Format Responses | Returns JSON and XML representations including errors using HTTP response codes. Supports CSV, PDF, PNG, and XLS for specific endpoints. |
| Cursor-Based Pagination | Collection resources support offset/limit pagination with limit range of 1-50 items per request with link relations. |
| Mock/Sandbox Testing | Demo subscriptions support custom response selection via X-Api-Mock-Scenario-ID and X-Api-Mock-Response headers. |
| Rate Limiting | Standard tier provides 100,000 calls per day and 100 calls per second for HIPAA transaction APIs. |
| ASC X12 EDI Standards | Full support for HIPAA EDI version 005010 transactions including 270/271, 276/277, 278, and 835 transaction sets. |

## Use Cases

| Name | Description |
|------|-------------|
| Real-Time Eligibility Verification | Verify patient insurance coverage, co-pays, deductibles, and benefits in real time before scheduling or rendering services. |
| Claim Status Tracking | Track submitted claims through adjudication, checking ACKNOWLEDGED, PENDING, PAID, DENIED, and ADJUSTED statuses. |
| Prior Authorization Management | Submit and track prior authorization requests using X12 278 transactions to check if authorization is required before service delivery. |
| Patient Cost Estimation | Estimate patient out-of-pocket costs before services are rendered to meet price transparency requirements and inform patients. |
| Electronic Claim Attachments | Electronically attach clinical documentation to claims and authorizations, reducing manual faxing and accelerating adjudication. |
| Care Gap Identification | Retrieve real-time care reminders during eligibility checks to identify preventive care gaps and coordinate outreach. |
| Digital Member ID Cards | Retrieve member ID cards digitally during eligibility verification, reducing administrative burden and improving patient experience. |
| Multi-Payer Data Consolidation | Connect to all major payers through a single clearinghouse API rather than managing individual payer connections. |

## Integrations

| Name | Description |
|------|-------------|
| EHR Systems | Integrates with electronic health record systems to embed eligibility and claims workflows into clinical workflows. |
| Practice Management Systems | Connects practice management software to payer networks for revenue cycle management and claims processing. |
| Revenue Cycle Management Platforms | Integrates with RCM platforms to automate eligibility verification, claim submission, and payment reconciliation. |
| Blue Cross Blue Shield Plans | Direct integration with BCBS plans nationwide for eligibility, claims, and prior authorization transactions. |
| Humana | Integration with Humana for care reminders, eligibility verification, and claims processing. |
| Molina Healthcare | Integration with Molina Healthcare for eligibility and benefits verification and care reminders. |
| Florida Blue | Integration with Florida Blue for care reminders and real-time eligibility verification. |
| Healthfirst New York | Integration with Healthfirst New York for eligibility and care gap identification. |

## Artifacts

Machine-readable API specifications organized by format.

### OpenAPI

- [Availity Eligibility & Benefits API](openapi/availity-eligibility-openapi.yml)
- [Availity Claim Status API](openapi/availity-claim-status-openapi.yml)
- [Availity Claim Attachments API](openapi/availity-claim-attachments-openapi.yml)
- [Availity Service Reviews API](openapi/availity-service-reviews-openapi.yml)

### JSON Schema

- [Eligibility Schema](json-schema/availity-eligibility-schema.json)
- [Claim Status Request Schema](json-schema/claim-status-claim-status-request-schema.json)
- [Claim Status Response Schema](json-schema/claim-status-claim-status-response-schema.json)
- [Service Review Request Schema](json-schema/service-reviews-service-review-request-schema.json)
- *(31 total JSON Schema files)*

### JSON-LD

- [Availity Eligibility Context](json-ld/availity-eligibility-context.jsonld)
- [Availity Claim Context](json-ld/availity-claim-context.jsonld)
- [Availity Service Context](json-ld/availity-service-context.jsonld)
- [Availity Attachments Context](json-ld/availity-attachments-context.jsonld)

## Capabilities

Naftiko capabilities organized as shared per-API definitions composed into customer-facing workflows.

### Shared Per-API Definitions

- [Eligibility & Benefits API](capabilities/shared/eligibility.yaml) — 4 operations for eligibility verification and payer lookup
- [Claim Status API](capabilities/shared/claim-status.yaml) — 4 operations for claim status inquiry and search
- [Service Reviews API](capabilities/shared/service-reviews.yaml) — 4 operations for prior authorization management

### Workflow Capabilities

| Workflow | APIs Combined | Tools | Persona |
|----------|--------------|-------|---------|
| [Healthcare Revenue Cycle Management](capabilities/availity-revenue-cycle-management.yaml) | Eligibility & Benefits, Claim Status, Service Reviews | 9 | Billing Specialist, Revenue Cycle Manager |

## Vocabulary

- [Availity Vocabulary](vocabulary/availity-vocabulary.yaml) — Unified taxonomy mapping 8 resources, 7 actions, 1 workflow, and 3 personas across operational (OpenAPI) and capability (Naftiko) dimensions

## Rules

- [Availity Spectral Rules](rules/availity-spectral-rules.yml) — 40 rules across 13 categories enforcing Availity API conventions

## Maintainers

**FN:** Kin Lane

**Email:** kin@apievangelist.com
