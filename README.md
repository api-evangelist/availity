# availity (availity)

Availity is a healthcare information network and clearinghouse providing REST APIs for real-time HIPAA EDI transactions. The platform processes over 11 billion annual healthcare transactions connecting providers, health plans, and vendors nationwide. Create your application and subscribe to a plan to make use of Availity APIs for eligibility verification, claims management, prior authorization, and patient cost estimation.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/availity/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/availity/refs/heads/main/apis.yml)

## Timestamps

- **Modified:** 2026-05-19

## APIs

### Availity Eligibility & Benefits API

The Availity Eligibility & Benefits API supports the ASC X12N 270 and 271 transactions, enabling real-time verification of member coverage, co-pays, deductibles, and benefits information. REST APIs connect provider systems to every major health plan nationwide for eligibility checks.

- **Human URL:** [https://developer.availity.com/](https://developer.availity.com/)
- **Base URL:** `https://api.availity.com`

#### Tags

- Benefits
- EDI
- Eligibility
- Healthcare
- X12 270/271

#### Properties

- [Documentation](https://developer.availity.com/partner/documentation)
- [Getting Started](https://developer.availity.com/partner/gettingstarted)
- [Documentation](https://developer.availity.com/blog/2025/3/4/ebvalue-add-api)
- [OpenAPI](https://raw.githubusercontent.com/api-evangelist/availity/refs/heads/main/openapi/availity-eligibility-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [JSON Schema](https://raw.githubusercontent.com/api-evangelist/availity/refs/heads/main/json-schema/availity-eligibility-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [Postman Collection](collections/availity-claim-attachments.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/availity-claim-attachments.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Postman Collection](collections/availity-claim-status.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/availity-claim-status.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Postman Collection](collections/availity-eligibility.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/availity-eligibility.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Availity Claim Status API

The Availity Claim Status API enables the standard ASC X12N 276 and 277 transactions, allowing providers to find, create, and manage claim status inquiries against payer systems. REST APIs bridge provider billing systems and payers through the Availity clearinghouse network. Supports both standard 276/277 workflows and enhanced claim status with summary and detail search.

- **Human URL:** [https://developer.availity.com/](https://developer.availity.com/)
- **Base URL:** `https://api.availity.com`

#### Tags

- Claims
- Clearinghouse
- EDI
- Healthcare
- X12 276/277

#### Properties

- [Documentation](https://developer.availity.com/partner/documentation)
- [Documentation](https://developer.availity.com/blog/2025/3/25/enhanced-claim-status)
- [Getting Started](https://developer.availity.com/partner/gettingstarted)
- [OpenAPI](https://raw.githubusercontent.com/api-evangelist/availity/refs/heads/main/openapi/availity-claim-status-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/availity-claim-attachments.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/availity-claim-attachments.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Postman Collection](collections/availity-claim-status.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/availity-claim-status.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Postman Collection](collections/availity-eligibility.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/availity-eligibility.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Availity Claim Attachments API

The Availity Claim Attachments API enables electronic submission of supporting documentation alongside healthcare claims. REST APIs support structured and unstructured attachment types for additional clinical information required by payers during claims adjudication.

- **Human URL:** [https://developer.availity.com/](https://developer.availity.com/)
- **Base URL:** `https://api.availity.com`

#### Tags

- Attachments
- Claims
- Clearinghouse
- EDI
- Healthcare

#### Properties

- [Documentation](https://developer.availity.com/blog/2025/2/28/claim-attachment-api)
- [Getting Started](https://developer.availity.com/partner/gettingstarted)
- [OpenAPI](https://raw.githubusercontent.com/api-evangelist/availity/refs/heads/main/openapi/availity-claim-attachments-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/availity-claim-attachments.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/availity-claim-attachments.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Postman Collection](collections/availity-claim-status.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/availity-claim-status.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Postman Collection](collections/availity-eligibility.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/availity-eligibility.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Availity Service Reviews (Prior Authorization) API

The Availity Service Reviews API enables the ASC X12N 278 transaction for prior authorization and healthcare service review. REST APIs allow providers to find, create, and manage authorization requests and responses with health plan payers through the Availity clearinghouse. Includes IsAuthRequired and Attachments add-on APIs.

- **Human URL:** [https://developer.availity.com/](https://developer.availity.com/)
- **Base URL:** `https://api.availity.com`

#### Tags

- EDI
- Healthcare
- Prior Authorization
- Service Reviews
- X12 278

#### Properties

- [Documentation](https://developer.availity.com/blog/2025/3/4/service-reviews)
- [Getting Started](https://developer.availity.com/partner/gettingstarted)
- [OpenAPI](https://raw.githubusercontent.com/api-evangelist/availity/refs/heads/main/openapi/availity-service-reviews-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/availity-claim-attachments.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/availity-claim-attachments.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Postman Collection](collections/availity-claim-status.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/availity-claim-status.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Postman Collection](collections/availity-eligibility.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/availity-eligibility.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Availity Healthcare HIPAA Transactions API

The Availity Healthcare HIPAA Transactions API provides a unified interface for standard HIPAA EDI transactions. REST APIs enable healthcare providers and vendors to submit and receive X12 EDI transactions across payers including eligibility, claims, remittance, authorizations, and referrals. Quota: 100,000 calls per day, 100 calls per second rate limit.

- **Human URL:** [https://developer.availity.com/portal/catalogue-products/healthcare-hipaa-transactions-1](https://developer.availity.com/portal/catalogue-products/healthcare-hipaa-transactions-1)
- **Base URL:** `https://api.availity.com`

#### Tags

- Clearinghouse
- EDI
- Healthcare
- HIPAA

#### Properties

- [Documentation](https://developer.availity.com/portal/catalogue-products/healthcare-hipaa-transactions-1)
- [Documentation](https://developer.availity.com/blog/2025/3/25/hipaa-transactions)
- [Getting Started](https://developer.availity.com/partner/gettingstarted)
- [Postman Collection](collections/availity-claim-attachments.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/availity-claim-attachments.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Postman Collection](collections/availity-claim-status.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/availity-claim-status.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Postman Collection](collections/availity-eligibility.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/availity-eligibility.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Availity Patient Cost Estimator API

The Availity Patient Cost Estimator API enables healthcare providers and institutions to estimate service costs before delivery for both institutional and professional services. REST APIs support version 1.0.0 and 2.0.0 and include predetermination requests across all major health plan payers, helping meet price transparency requirements.

- **Human URL:** [https://developer.availity.com/](https://developer.availity.com/)
- **Base URL:** `https://api.availity.com`

#### Tags

- Cost Estimation
- Healthcare
- Patient Financial Responsibility
- Price Transparency

#### Properties

- [Documentation](https://developer.availity.com/partner/documentation)
- [Getting Started](https://developer.availity.com/partner/gettingstarted)
- [Postman Collection](collections/availity-claim-attachments.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/availity-claim-attachments.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Postman Collection](collections/availity-claim-status.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/availity-claim-status.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Postman Collection](collections/availity-eligibility.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/availity-eligibility.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Availity Eligibility & Benefits Value-Add APIs

The Availity Eligibility & Benefits Value-Add APIs provide supplementary data during eligibility transactions. The Care Reminders API retrieves real-time care gap information from multiple payers. The Member ID Card API retrieves digital member ID cards in PDF or PNG format during eligibility verification workflows.

- **Human URL:** [https://developer.availity.com/](https://developer.availity.com/)
- **Base URL:** `https://api.availity.com`

#### Tags

- Care Reminders
- EDI
- Eligibility
- Healthcare
- Member ID Card

#### Properties

- [Documentation](https://developer.availity.com/blog/2025/3/4/ebvalue-add-api)
- [Getting Started](https://developer.availity.com/partner/gettingstarted)
- [Postman Collection](collections/availity-claim-attachments.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/availity-claim-attachments.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Postman Collection](collections/availity-claim-status.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/availity-claim-status.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Postman Collection](collections/availity-eligibility.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/availity-eligibility.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Availity Payer List API

The Availity Payer List API (v1.0.4) allows healthcare organizations to query available payers and the transactions they support. Returns payer identifiers, names, and supported transaction types including eligibility, claim status, prior authorization, and remittance across the nationwide Availity clearinghouse network.

- **Human URL:** [https://developer.availity.com/](https://developer.availity.com/)
- **Base URL:** `https://api.availity.com`

#### Tags

- Clearinghouse
- Healthcare
- Payer Network
- Reference Data

#### Properties

- [Documentation](https://developer.availity.com/partner/documentation)
- [Getting Started](https://developer.availity.com/partner/gettingstarted)
- [Postman Collection](collections/availity-claim-attachments.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/availity-claim-attachments.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Postman Collection](collections/availity-claim-status.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/availity-claim-status.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Postman Collection](collections/availity-eligibility.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/availity-eligibility.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Availity Configurations API

The Availity Configurations API (v1.0.0) provides provider details and payer-specific validation requirements. Returns configuration rules for enhanced claim status, prior authorization, and other transaction types so provider systems can validate submissions before sending to payers.

- **Human URL:** [https://developer.availity.com/](https://developer.availity.com/)
- **Base URL:** `https://api.availity.com`

#### Tags

- Configuration
- Healthcare
- Payer Requirements
- Provider Validation

#### Properties

- [Documentation](https://developer.availity.com/partner/documentation)
- [Getting Started](https://developer.availity.com/partner/gettingstarted)
- [Postman Collection](collections/availity-claim-attachments.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/availity-claim-attachments.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Postman Collection](collections/availity-claim-status.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/availity-claim-status.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Postman Collection](collections/availity-eligibility.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/availity-eligibility.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [LinkedIn](https://www.linkedin.com/company/availity)
- [Website](https://www.availity.com)
- [Portal](https://developer.availity.com/)
- [Documentation](https://developer.availity.com/partner/documentation)
- [Getting Started](https://developer.availity.com/partner/gettingstarted)
- [Documentation](https://developer.availity.com/blog/2025/3/25/availity-api-guide)
- [Support](https://developer.availity.com/partner/contact-us)
- [Terms of Service](https://www.availity.com/terms-of-use/)
- [Privacy Policy](https://www.availity.com/Privacy-Policy/)
- [GitHub Organization](https://github.com/availity)
- [SDK](https://availity.github.io/sdk-js/)
- [OpenAPI](https://raw.githubusercontent.com/api-evangelist/availity/refs/heads/main/openapi/availity-eligibility-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [OpenAPI](https://raw.githubusercontent.com/api-evangelist/availity/refs/heads/main/openapi/availity-claim-status-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [OpenAPI](https://raw.githubusercontent.com/api-evangelist/availity/refs/heads/main/openapi/availity-claim-attachments-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [OpenAPI](https://raw.githubusercontent.com/api-evangelist/availity/refs/heads/main/openapi/availity-service-reviews-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [JSON Schema](https://raw.githubusercontent.com/api-evangelist/availity/refs/heads/main/json-schema/availity-eligibility-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON-LD](https://raw.githubusercontent.com/api-evangelist/availity/refs/heads/main/json-ld/availity-eligibility-context.jsonld) — [JSON-LD](https://www.w3.org/TR/json-ld11/)
- [JSON-LD](https://raw.githubusercontent.com/api-evangelist/availity/refs/heads/main/json-ld/availity-claim-context.jsonld) — [JSON-LD](https://www.w3.org/TR/json-ld11/)
- [JSON-LD](https://raw.githubusercontent.com/api-evangelist/availity/refs/heads/main/json-ld/availity-service-context.jsonld) — [JSON-LD](https://www.w3.org/TR/json-ld11/)
- [Spectral Rules](https://raw.githubusercontent.com/api-evangelist/availity/refs/heads/main/rules/availity-spectral-rules.yml)
- [Vocabulary](https://raw.githubusercontent.com/api-evangelist/availity/refs/heads/main/vocabulary/availity-vocabulary.yaml)
- [Features](undefined)
- [Use Cases](undefined)
- [Integrations](undefined)
- [L L Ms Txt](https://developer.availity.com/llms.txt)

## Maintainers

**Email:** kin@apievangelist.com
