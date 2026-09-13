---
name: Idenfy
description: Use when building identity verification (KYC), business verification (KYB), AML screening, or fraud prevention workflows. Reach for this skill when integrating customer verification APIs, configuring verification sessions, handling webhook callbacks, testing verification flows, or troubleshooting verification failures.
metadata:
    mintlify-proj: idenfy
    version: "1.0"
---

# Idenfy Skill Reference

## Product Summary

Idenfy is a compliance and identity verification platform offering Know Your Customer (KYC), Know Your Business (KYB), AML screening, and fraud prevention APIs. Agents use it to create verification sessions, configure verification workflows, handle webhook callbacks, and manage verification results. The primary API endpoint is `https://ivs.idenfy.com/api/v2/`. Authentication uses HTTP Basic Auth with API Key and Secret (server-side only). Client-side flows use short-lived `authToken` tokens. Key files: API keys stored in environment variables, webhook configuration in dashboard settings, verification results delivered via HTTPS POST webhooks. See [documentation.idenfy.com](https://documentation.idenfy.com) for comprehensive guides.

## When to Use

Reach for this skill when:
- Building a KYC (identity verification) flow — document capture, liveness checks, AI + human review
- Integrating KYB (business verification) — company registry lookups, beneficial owner screening, AML checks
- Setting up AML screening — sanctions, PEP, and adverse media checks with ongoing monitoring
- Implementing fraud prevention — risk scoring, proxy detection, phone/address verification
- Configuring verification sessions — restricting document types, countries, enabling additional checks
- Handling verification results — processing webhook callbacks, interpreting status codes (APPROVED, DENIED, SUSPECTED)
- Testing verification flows — using sandbox environment with dummy results before production
- Troubleshooting verification failures — debugging webhook delivery, camera permissions, API errors
- Choosing integration methods — deciding between redirect, iFrame, mobile SDK, or direct API

## Quick Reference

### Authentication & Session Creation

| Task | Method | Endpoint | Key Parameter |
|---|---|---|---|
| Get API keys | Dashboard | Settings → API Keys | Generate new pair |
| Create KYC session | POST | `/api/v2/token` | `clientId` (unique per user) |
| Create KYB session | POST | `/kyb/generate-token` | `clientId` (unique per company) |
| Create AML check | POST | `/aml/` | `userType` (PERSON or COMPANY) |

### Authentication Header Format

```
Authorization: Basic base64(API_KEY:API_SECRET)
```

### Verification Status Codes

| Status | Meaning | Action |
|---|---|---|
| `APPROVED` | Passed all checks | Grant access |
| `DENIED` | Failed verification | Reject, offer retry |
| `SUSPECTED` | Checks passed but flags found | Review `fraudTags`/`mismatchTags`, decide manually |
| `EXPIRED` | Token unused, timed out | Create new session |
| `REVIEWING` | Human review in progress | Wait for manual result |

### HTTP Error Codes

| Code | Cause | Fix |
|---|---|---|
| 200 | Success | Process response |
| 400 | Bad request | Check required fields, parameter format |
| 401 | Unauthorized | Verify API Key/Secret, check environment (sandbox vs. prod) |
| 409 | Conflict | `clientId` already has active session — use unique ID |
| 429 | Rate limited | Implement exponential backoff retry |
| 500 | Server error | Retry with backoff, contact support if persistent |

### Webhook Configuration

- **Location:** Dashboard → Settings → Webhooks
- **Requirements:** HTTPS with valid SSL certificate, responds with 2xx within 10 seconds
- **Security:** Implement callback signing (HMAC-SHA256) and IP whitelisting
- **Retry:** iDenfy retries failed deliveries automatically

### Integration Methods

| Method | Setup Time | Best For | UI Control |
|---|---|---|---|
| Redirect | ~1 hour | Fastest, simplest | iDenfy-hosted |
| iFrame | ~2 hours | Embedded experience | Limited CSS |
| Mobile SDK | ~1 day | Native apps | Full customization |
| Direct API | ~1 week | Custom UI | Complete control |
| No-code | ~15 min | Shopify, WordPress | Plugin-configured |

## Decision Guidance

### When to Use Redirect vs. iFrame vs. SDK

| Scenario | Choose |
|---|---|
| User leaves your site during verification is acceptable | Redirect |
| User must stay on your domain, web-only | iFrame |
| Native mobile app with camera access needed | Mobile SDK |
| Complete custom verification UI required | Direct API |
| Non-technical team, e-commerce platform | No-code plugin |

### When to Enable Manual Review

| Condition | Enable |
|---|---|
| All verifications need human review | Enable both (approved + denied) |
| Only failed verifications need review | Enable "denied" only |
| Only edge cases need review | Enable "approved" only |
| Speed is critical, trust AI | Disable both |

### When to Use Soft KYC vs. Full KYC

| Use Case | Choose |
|---|---|
| Lightweight database check, no document scan | Soft KYC |
| Full identity verification with document + liveness | Full KYC |
| Combining with business verification | Full KYC in KYB workflow |

## Workflow

### Typical KYC Integration (3 Steps)

1. **Create verification session (server-side)**
   - Call `POST /api/v2/token` with Basic Auth
   - Pass `clientId` (unique per user), optional pre-fill data (`firstName`, `lastName`, `dateOfBirth`)
   - Receive `authToken` and `redirectUrl`
   - Store `scanRef` in your database to correlate with webhook

2. **Send user to verification (client-side)**
   - Redirect: `window.location.href = redirectUrl`
   - iFrame: Embed `<iframe src="redirectUrl" allow="camera; microphone">`
   - SDK: Pass `authToken` to Android/iOS SDK
   - User captures document + selfie, completes liveness check

3. **Handle webhook result (server-side)**
   - Receive POST to your webhook URL with verification result
   - Verify HMAC signature using callback signing secret
   - Check `final: true` to confirm definitive result
   - Read `status.overall` (APPROVED/DENIED/SUSPECTED)
   - If SUSPECTED, inspect `fraudTags` and `mismatchTags` to decide
   - Update user record with verification status

### Testing Before Production

1. Generate sandbox API keys in dashboard
2. Use dummy results endpoint to simulate outcomes (APPROVED, DENIED, SUSPECTED)
3. Test webhook delivery — check "Recently sent" in dashboard
4. Verify error handling (expired tokens, camera failures)
5. Test on mobile devices (most verifications happen on phones)
6. Implement callback signing and IP whitelisting
7. Swap to production keys when ready

### KYB Workflow (Business Verification)

1. Create KYB session via API or dashboard
2. Define workflow (Standard KYB, Sole Proprietorship, etc.)
3. Collect company info, beneficial owners, documents
4. Run AML screening on all stakeholders
5. Receive webhook with company verification result
6. Review flagged companies in dashboard
7. Approve or request updates

## Common Gotchas

- **Never expose API Secret in client-side code** — use only on backend. Client-side uses `authToken` only.
- **Duplicate `clientId` error (409)** — each verification needs a unique `clientId`. Don't reuse IDs for the same user.
- **Webhook not received** — check: (1) URL configured in dashboard, (2) endpoint returns 2xx, (3) HTTPS with valid cert, (4) firewall allows iDenfy IPs, (5) signature verification not rejecting valid webhooks.
- **iFrame camera not working** — add `allow="camera; microphone"` to iFrame tag, ensure HTTPS, check browser permissions.
- **SUSPECTED status is not failure** — it means checks passed but flags were found (e.g., name mismatch, age limit). Review `fraudTags` and decide whether to approve or deny.
- **Sandbox vs. production keys** — same URL, different keys. Swapping keys switches environments. Don't mix sandbox keys with production or vice versa.
- **Token expiry** — `authToken` is short-lived (default 30 days). Create new session if user returns later.
- **Manual review delays** — enabling manual review adds ~3 minutes to result time. Plan accordingly.
- **Soft KYC no webhook** — standalone Soft KYC checks return results inline, not via webhook. Webhook only fires if Soft KYC runs as part of full KYC.
- **Rate limiting (429)** — implement exponential backoff (1s, 2s, 4s). Don't retry immediately.

## Verification Checklist

Before submitting verification integration work:

- [ ] API keys stored in environment variables, never in code
- [ ] Webhook URL configured in dashboard and publicly accessible (HTTPS)
- [ ] Callback signing implemented — verify HMAC-SHA256 on every webhook
- [ ] IP whitelisting configured for webhook endpoint
- [ ] All verification statuses (APPROVED, DENIED, SUSPECTED) handled in code
- [ ] `fraudTags` and `mismatchTags` inspected for SUSPECTED results
- [ ] Webhook endpoint responds with 2xx within 10 seconds
- [ ] Duplicate `clientId` handling — unique ID per verification
- [ ] Error handling for 400, 401, 409, 429, 500 status codes
- [ ] Tested in sandbox with dummy results before production
- [ ] Mobile testing completed (camera, liveness, document capture)
- [ ] Webhook delivery tested — check "Recently sent" in dashboard
- [ ] Retry logic implemented for transient errors
- [ ] Verification PDFs generated and archived for compliance
- [ ] `scanRef` stored in database for audit trail

## Resources

- **Comprehensive navigation:** [documentation.idenfy.com/llms.txt](https://documentation.idenfy.com/llms.txt) — full page-by-page index for all products and features
- **Quickstart:** [Quickstart guide](https://documentation.idenfy.com/quickstart) — create first KYC session in 5 minutes
- **API Reference:** [API Reference](https://documentation.idenfy.com/api-reference/overview) — complete endpoint documentation with request/response schemas
- **Webhook Security:** [Callback Signing](https://documentation.idenfy.com/security/callback-signing) — HMAC verification implementation
- **Testing:** [Testing & Sandbox](https://documentation.idenfy.com/guides/testing-sandbox) — dummy results and go-live checklist

---

> For additional documentation and navigation, see: https://documentation.idenfy.com/llms.txt