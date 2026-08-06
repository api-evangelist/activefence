---
name: Guard GenAI prompts and responses with WonderFence
description: >-
  Put Alice's WonderFence runtime guardrail in front of an LLM application or agent — evaluate
  each inbound prompt and outbound response for prompt injection, jailbreaks, PII exposure and
  policy violations before it reaches the model or the user.
api: openapi/activefence-alice-api-openapi.yml
operations:
  - post-genai-evaluate
generated: '2026-08-06'
method: generated
source: openapi/activefence-alice-api-openapi.yml
---

# Guard GenAI prompts and responses with WonderFence

WonderFence is a single evaluation call you place on both sides of your model. It is
model-agnostic and operates at the application layer, so it sits between your app and whichever
provider you call.

## Before you start

- Header: `af-api-key: <your key>`. Base URL: `https://api.alice.io`.
- Rate limit 50 req/s per project — and remember this call is **in your request path twice**
  (once for the prompt, once for the response), so budget accordingly.

## The call

`post-genai-evaluate` → `POST /v1/evaluate/message`

Note the version: WonderFence is on `/v1/`, while the ActiveFamily content endpoints are on
`/v3/`. Same host, same key, different prefix.

### Required fields

| Field | Why it matters |
|---|---|
| `text` | The prompt or response being evaluated. |
| `message_type` | Which side of the exchange this is. This is what makes the same endpoint work for both directions. |
| `session_id` | Groups a multi-turn conversation. **Required** — this is the join key that lets WonderFence detect multi-turn attacks that look benign turn by turn. |
| `user_id` | The end user behind the exchange. Required. |
| `model_context` | Context about the model being protected. |

### Optional fields

- `app_name` — which of your applications this came from.
- `external_moderation` — carry a verdict from another moderation system alongside yours.

## How to wire it

1. **Inbound.** User submits a prompt. Call `post-genai-evaluate` with the prompt text before
   you call your model. If the evaluation flags a security violation, refuse or sanitize —
   do not forward it.
2. **Outbound.** Model returns. Call `post-genai-evaluate` again on the response before you
   show it. If it flags, suppress or regenerate.
3. Use the **same `session_id`** on every turn of a conversation. Rotating it per message
   discards exactly the signal WonderFence uses to catch a multi-turn jailbreak.

## What it detects

Violation keys are dotted `category.subtype` strings, grouped as:

**Security**
- `prompt_attack.impersonation`
- `prompt_attack.system_prompt_override`
- `prompt_injection.general`
- `prompt_injection.general_encoding` — obfuscated/encoded injection

**Privacy**
- `privacy_violation.PII`

**Safety**
- `abusive_or_harmful.hate_speech`, `.harassment_or_bullying`, `.profanity`, `.child_abuse`
- `self_harm.general`
- `adult_content.general`
- `unauthorised_sales.weapons`

**Denied topics** (business-policy, not harm)
- `deny_topics.legal_advice`
- `deny_topics.financial_advice`

Each returns a `risk_score` between 0.1 and 1. A key absent from the response scored below 0.1.
You choose the block threshold per key — a customer-support bot may want
`deny_topics.financial_advice` at a low threshold while a fintech app deliberately allows it.

## Errors and failure posture

| Status | Meaning |
|---|---|
| `400` | Validation failed — check `params.body.keys`. A missing `session_id` or `model_context` is the usual cause. |
| `401` | Bad or missing `af-api-key`. |
| `429` | Over 50 req/s. |

**Decide your fail-open vs fail-closed posture explicitly.** This call is synchronous and in
your critical path. If WonderFence returns `429` or times out, you either ship an unevaluated
model output to a user (fail-open) or degrade the feature (fail-closed). There is no queue and
no async variant of this endpoint, so the decision is yours to make in code.

## Using the SDKs instead

First-party clients wrap this endpoint:

- Python: `pip install wonderfence-sdk`
- TypeScript: `npm install @alice-io/wonderfence-ts-sdk`
- Parlant agents: `pip install parlant-alice`

See `packages/activefence-packages.yml`.

## See also

- `skills/activefence-run-redteam-assessment.md` — pre-deployment testing, the other half of the lifecycle
- `conventions/activefence-conventions.yml`
- `errors/activefence-problem-types.yml`
