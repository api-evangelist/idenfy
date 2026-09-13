# Archived OpenAPI definitions — superseded 2026-09-13

The files in this directory carry the suffix `-SCAFFOLD-superseded` because they
describe endpoints iDenfy does not publish.

`idenfy-openapi-SCAFFOLD-superseded.yml` (added 2026-08-03, recorded in
`provenance.yml` as "harvested") was checked against iDenfy's own published
contracts on 2026-09-13 and does not match them:

| Scaffold path                  | iDenfy's published path                                   |
| ------------------------------ | --------------------------------------------------------- |
| `POST /kyc/sessions`           | `POST /api/v2/token`                                      |
| `POST /kyb/sessions`           | `POST /kyb/tokens/`                                       |
| `POST /bank/sessions`          | `POST /bank/tokens/`                                      |
| `POST /aml/checks`             | `POST /aml/checks/`  (trailing slash; different body)     |
| `POST /fraud/risk-assessment`  | `POST /risk/assessments/`                                 |
| `POST /fraud/phone-validation` | `POST /fraud/validate-phone`                              |
| `POST /fraud/phone-verification` | `POST /fraud/send-sms` + `POST /fraud/verify-sms`       |
| `POST /fraud/address-verification` | `POST /api/v2/address-verification`                   |

Sources for the real paths: https://documentation.idenfy.com/openapi/*.yaml and the
Fraud Prevention reference pages under https://documentation.idenfy.com/fraud-prevention/.

The seven first-party OpenAPI 3.1.0 documents iDenfy publishes are now in
`openapi/_original/` (verbatim) and `openapi/`.

`collections/_archive/` holds the Postman/OpenCollection files that were derived
from this scaffold and inherit the same wrong paths.
