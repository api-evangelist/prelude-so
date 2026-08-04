# Prelude (prelude-so)

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
