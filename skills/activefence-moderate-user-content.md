---
name: Moderate user-generated content with ActiveScore
description: >-
  Submit text, image, video or audio from your platform to Alice (formerly ActiveFence) and act
  on the returned per-violation risk scores. Covers the synchronous path for pre-publish gating
  and the asynchronous callback path for heavier media.
api: openapi/activefence-alice-api-openapi.yml
operations:
  - post-sync-content-text
  - post-sync-content-bulk-text
  - post-sync-content-image
  - post-content-text
  - post-content-image
  - post-content-video
  - post-content-audio
generated: '2026-08-06'
method: generated
source: openapi/activefence-alice-api-openapi.yml
---

# Moderate user-generated content with ActiveScore

## Before you start

- Every request carries the header `af-api-key: <your key>`. There is no OAuth and no bearer
  token. Keys are issued in the Alice console under **Account Settings → DATA MANAGEMENT →
  Alice API Keys**, and the value is shown once only.
- Base URL is `https://api.alice.io`.
- Default rate limit is **50 requests/second per project**. Over the limit you get `429`. Alice
  publishes no `RateLimit-*` or `Retry-After` headers, so implement your own backoff.

## Choose synchronous or asynchronous

Pick by whether you can hold a connection open for the answer.

**Synchronous** — use when you are gating a publish and need the verdict inline.
Only text and image have synchronous variants.

| Need | Operation | Path |
|---|---|---|
| One text item | `post-sync-content-text` | `POST /sync/v3/content/text` |
| Many text items at once | `post-sync-content-bulk-text` | `POST /sync/v3/content/bulk/text` |
| One image | `post-sync-content-image` | `POST /sync/v3/content/image` |

Expect p50 ~100ms / p90 ~250ms for text, and p50 ~1s / p90 ~5s for image (server-side,
excluding network).

**Asynchronous** — required for video and audio, and available for text and image. You get an
acknowledgement immediately and the analysis arrives later at a callback URL.

| Media | Operation | Path |
|---|---|---|
| Text | `post-content-text` | `POST /v3/content/text` |
| Image | `post-content-image` | `POST /v3/content/image` |
| Video | `post-content-video` | `POST /v3/content/video` |
| Audio | `post-content-audio` | `POST /v3/content/audio` |

Async is slow for long media by design — a 30-minute video is p90 ~3.5 minutes and 30 minutes
of audio is p90 ~20 minutes. Never block a user-facing request on it.

## Step 1 — submit the item

`text` and `content_id` are required on `post-content-text` and `post-sync-content-text`.
`content_id` is **your** identifier for the item; Alice does not mint one.

Optional context fields materially improve the analysis, so send what you have:
`category`, `user_id` (who authored it), `contained_in` (the collection it lives in),
`webpage_url`, `date_created`, `views_count`, `comments_count`, `title`, `description`,
`thumbnail_url`.

Use `custom_fields` for your own attributes, and `response_custom_fields` when you want values
echoed back to you on the result — that is the clean way to round-trip your own correlation
data through an async callback.

## Step 2 (async only) — register the callback

On any async operation, set:

- `callback_url` — the endpoint Alice will `POST` the completed analysis to.
- `callback_key_name` — the name of a key you defined in the platform's **Auth Management**
  section. Alice injects that key into the header or query params of the callback so your
  endpoint can authenticate the caller.

There is **no HMAC signature and no timestamp** on the callback. The shared key is the only
authentication. Treat the callback endpoint accordingly — do not act on an unauthenticated POST.

## Step 3 — read the acknowledgement, and honour `analyzed_violations`

An async `200` returns `response_id` plus `analyzed_violations[]` — the violation types that
*will* be analyzed for this item, given your account configuration and the media type.

**If `analyzed_violations` comes back empty, no callback will ever be sent.** Resolve the
pending record immediately instead of leaving it waiting. This is the most common integration
bug on this API.

`response_id` is your correlation key: every callback for a request carries the same value.

## Step 4 — interpret the result

The analysis returns `violation_types[]`, each with a `risk_score`.

- `risk_score` is a number **between 0.1 and 1** — the probability the item violates that
  violation type. A violation type is only returned when its score clears 0.1, so absence
  means "below threshold", not "checked and clean".
- The console renders this 0–100 and aggregates it to one number per item. The API does not —
  you get the per-violation array and decide how to combine it.
- `detection_type` appears **only** with the value `manual`, meaning a human reviewer in the
  Alice console made that decision rather than a model. Treat a `manual` verdict as
  authoritative over a model score.
- `language` and `confidence` come back alongside the scores.

Violation type keys are dotted `category.subtype` strings, for example
`abusive_or_harmful.hate_speech`, `abusive_or_harmful.harassment_or_bullying`,
`abusive_or_harmful.child_abuse`, `self_harm.general`, `adult_content.general`,
`unauthorised_sales.weapons`, `privacy_violation.PII`.

Set your own action thresholds per violation type. Alice returns probabilities, not decisions.

## Errors

| Status | Meaning | What to do |
|---|---|---|
| `400` | Validation failed | Read `params.body.keys` for the offending fields and `params.body.message` for the reason. Not retryable unchanged. |
| `401` | Bad or missing `af-api-key` | Check the header. If you just rotated, the old key dies 12 hours after regeneration. |
| `429` | Over 50 req/s | Back off. No `Retry-After` is sent — use your own schedule. |

The error envelope is plain `application/json`, **not** RFC 9457 problem+json:
`{statusCode, error, message, params: {body: {source, keys[], message}}}`.

No `403`, `404` or `5xx` responses are declared in the spec. Handle them defensively anyway.

## Idempotency

There is none. Alice publishes no `Idempotency-Key` header and no idempotency contract.
**Re-sending the same `content_id` creates a new analysis with a new `response_id`** — it does
not de-duplicate. If a submission times out, decide deliberately whether to retry, and
de-duplicate on your own side using `content_id`.

## See also

- `conventions/activefence-conventions.yml` — full cross-cutting semantics
- `errors/activefence-problem-types.yml` — error catalog
- `asyncapi/activefence-webhooks.yml` — callback and action-webhook surface
