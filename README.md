# Prelude (prelude-so)

Prelude is a phone and email verification API - "the trust layer between your signups and your business." Its **Verify** API creates and checks one-time passcodes (OTP) across SMS, WhatsApp, RCS, Viber, and voice in 230+ countries, using smart multi-provider routing (30+ providers, automatic failover) and built-in anti-fraud to keep spend on genuine users. Prelude markets itself as a developer-first alternative to Twilio Verify. Alongside Verify it offers **Notify** (transactional messaging), **Lookup / Intel** (phone number intelligence), and **Watch** (anti-fraud risk prediction and feedback).

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/prelude-so/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/prelude-so/refs/heads/main/apis.yml)

## Access Model

- **Public, documented REST API.** All products share the base URL `https://api.prelude.dev/v2` and are documented publicly at [docs.prelude.so](https://docs.prelude.so).
- **Authentication:** Bearer API key - `Authorization: Bearer YOUR_API_KEY`. Keys are issued from the Prelude dashboard (All Services > Configure > Keys). Self-service signup is available; a free trial credit is offered and paid usage is Pay-As-You-Go with no minimum commitment.
- **SDKs:** Official SDKs for Python, Node.js, Java, and Go, plus frontend SDKs (mobile / web) that produce a `dispatch_id` feeding the anti-fraud (Watch) signals.
- **No documented public WebSocket API.** Prelude's public surface is request/response REST over HTTPS. Asynchronous delivery status is returned via webhook `callback_url` callbacks, not a client-facing socket. See `review.yml`.

The endpoint paths and request/response schemas in this repository are grounded in the live Prelude documentation at docs.prelude.so as of 2026-07-11. The Watch `dispatch-events` endpoint is referenced in the docs but its full schema was not published at review time, so it is modeled and flagged (`x-modeled`) in the OpenAPI definition.

## Tags

- Number Verification
- Phone Verification
- OTP
- Authentication
- Anti-Fraud
- Two-Factor Authentication
- SMS
- Phone Number Lookup

## Timestamps

- **Created:** 2026-07-11
- **Modified:** 2026-07-11

## APIs

### Prelude Verification API

Create or retry a one-time passcode (OTP) verification for a phone number or email address and check the submitted code. Delivery spans SMS, WhatsApp, RCS, Viber, and voice with smart multi-provider routing, optional PSD2 dynamic linking on check, and inline anti-fraud signals.

- **Human URL:** [https://docs.prelude.so/verify/v2/api-reference/create-or-retry-a-verification](https://docs.prelude.so/verify/v2/api-reference/create-or-retry-a-verification)
- **Base URL:** `https://api.prelude.dev/v2`
- `POST /verification` - create or retry a verification
- `POST /verification/check` - check a code

### Prelude Lookup API

Phone number intelligence (Intel). Look up an E.164 number to get its line type, current and original carrier / network info (name, MCC, MNC), ported and temporary flags, and optionally the caller name (CNAM).

- **Human URL:** [https://docs.prelude.so/intel/v2/api-reference](https://docs.prelude.so/intel/v2/api-reference)
- **Base URL:** `https://api.prelude.dev/v2`
- `GET /lookup/{phone_number}` - look up a phone number

### Prelude Watch Anti-Fraud API

Predict whether a signup identifier is legitimate or suspicious using device, network, and behavioral signals, then send feedback about what actually happened in your verification flow so the model improves.

- **Human URL:** [https://docs.prelude.so/watch/v2/api-reference](https://docs.prelude.so/watch/v2/api-reference)
- **Base URL:** `https://api.prelude.dev/v2`
- `POST /watch/predict` - predict signup risk
- `POST /watch/feedback` - send feedbacks about verifications
- `POST /watch/dispatch-events` - dispatch frontend SDK events (modeled; schema unconfirmed)

### Prelude Transactional Messaging API

Transactional messaging (Notify). Send a template-based message to a recipient over the best available channel (SMS, RCS, or WhatsApp), with variables, scheduling, expiry, delivery callbacks, media documents, and auto-retries.

- **Human URL:** [https://docs.prelude.so/notify/v2/api-reference](https://docs.prelude.so/notify/v2/api-reference)
- **Base URL:** `https://api.prelude.dev/v2`
- `POST /notify` - send a transactional message

## Common Properties

- [Authentication](authentication/prelude-so-authentication.yml)
- [LinkedIn](https://www.linkedin.com/company/prelude-so)
- [Website](https://prelude.so)
- [Documentation](https://docs.prelude.so)
- [Plans](plans/prelude-so-plans-pricing.yml)
- [Rate Limits](rate-limits/prelude-so-rate-limits.yml)
- [Fin Ops](finops/prelude-so-finops.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
