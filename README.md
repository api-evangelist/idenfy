# iDenfy (idenfy)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

iDenfy is an identity verification platform providing KYC, KYB, and AML compliance solutions. The iDenfy API enables businesses to verify identities, check for fraud, and comply with regulatory requirements through automated document verification, facial recognition, AML screening, business verification, and bank verification services.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/idenfy/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/idenfy/refs/heads/main/apis.yml)

## Scope

- **Type:** Index

## Tags

- AML
- Compliance
- Fraud Detection
- Identity Verification
- KYB
- KYC

## Timestamps

- **Created:** 2024-11-13
- **Modified:** 2026-04-28

## APIs

### iDenfy Identity Verification API

The iDenfy Identity Verification (KYC) API provides document verification, selfie checks, and liveness detection through redirect, iFrame, mobile SDK, or direct API integration.

- **Human URL:** [https://documentation.idenfy.com/](https://documentation.idenfy.com/)

#### Tags

- Identity Verification
- KYC
- Liveness

#### Properties

- [Documentation](https://documentation.idenfy.com/)
- [Postman Collection](collections/idenfy.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/idenfy.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### iDenfy Business Verification API

The iDenfy Business Verification (KYB) API enables company verification using registry lookups, ultimate beneficial owner identification, and credit report checks via redirect or iFrame integration.

- **Human URL:** [https://documentation.idenfy.com/](https://documentation.idenfy.com/)

#### Tags

- Business Verification
- KYB
- UBO

#### Properties

- [Documentation](https://documentation.idenfy.com/)
- [Postman Collection](collections/idenfy.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/idenfy.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### iDenfy AML Screening API

The iDenfy AML Screening API screens individuals and companies against sanctions lists, politically exposed persons (PEPs), and adverse media, with one-time and ongoing monitoring options.

- **Human URL:** [https://documentation.idenfy.com/](https://documentation.idenfy.com/)

#### Tags

- AML
- Compliance
- PEP
- Sanctions

#### Properties

- [Documentation](https://documentation.idenfy.com/)
- [Postman Collection](collections/idenfy.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/idenfy.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### iDenfy Fraud Prevention API

The iDenfy Fraud Prevention API provides risk scoring, proxy detection, phone and address verification, and proof of address checks to identify and stop fraudulent activities.

- **Human URL:** [https://documentation.idenfy.com/fraud/FraudApi/](https://documentation.idenfy.com/fraud/FraudApi/)

#### Tags

- Fraud Detection
- Identity Verification
- Risk Scoring

#### Properties

- [Documentation](https://documentation.idenfy.com/fraud/FraudApi/)
- [Postman Collection](collections/idenfy.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/idenfy.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### iDenfy Face Authentication API

The iDenfy Face Authentication API re-authenticates returning users by comparing a live facial scan against a previously verified identity.

- **Human URL:** [https://documentation.idenfy.com/](https://documentation.idenfy.com/)

#### Tags

- Biometrics
- Face Authentication
- Identity Verification

#### Properties

- [Documentation](https://documentation.idenfy.com/)
- [Postman Collection](collections/idenfy.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/idenfy.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### iDenfy Bank Verification API

The iDenfy Bank Verification API verifies bank accounts via open banking connections to over 2,500 European banks.

- **Human URL:** [https://documentation.idenfy.com/](https://documentation.idenfy.com/)

#### Tags

- Bank Verification
- Open Banking

#### Properties

- [Documentation](https://documentation.idenfy.com/)
- [Postman Collection](collections/idenfy.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/idenfy.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [GitHub Organization](https://github.com/idenfy)
- [LinkedIn](https://www.linkedin.com/company/idenfy)
- [Website](https://www.idenfy.com/)
- [Documentation](https://documentation.idenfy.com/)
- [Support](https://www.idenfy.com/contact/)
- [Integrations](https://idenfy.com/integrations/)
- [L L Ms Txt](https://idenfy.com/llms.txt)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
