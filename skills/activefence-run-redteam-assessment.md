---
name: Run a WonderBuild red-team assessment
description: >-
  Drive Alice's WonderBuild pre-deployment adversarial testing from CI — list assessments,
  launch one from a preset, re-run or clone an existing one, and poll for completion.
api: openapi/activefence-alice-api-openapi.yml
operations:
  - get-assessments
  - run-assessment
  - clone-and-run-assessment
  - run-assessment-preset
generated: '2026-08-06'
method: generated
source: openapi/activefence-alice-api-openapi.yml
---

# Run a WonderBuild red-team assessment

WonderBuild runs adversarial testing against a GenAI application before it ships — prompt
injection, jailbreaks, unsafe behavior, data leakage, policy violations. These four operations
are enough to wire it into a release gate.

## Before you start

- Header: `af-api-key: <your key>`. Base URL: `https://api.alice.io`.
- These paths are **unversioned** — `/redteam/...`, with no `/v1/` or `/v3/` segment, unlike
  the rest of the API. Do not assume a version prefix.
- The application under test **must already be configured in the Alice platform**. There is no
  public API to register one; do it in the console first.

## Launch an assessment

### From a preset — the CI entry point

`run-assessment-preset` → `POST /redteam/assessments/runFromPreset`

All three body fields are required:

| Field | Notes |
|---|---|
| `preset_name` | The preset to build the assessment from, e.g. `all_safety_checks`. |
| `app_name` | Must match an app already configured in Alice, e.g. `MyChatBot`. |
| `version_name` | e.g. `1.2`. **If this version does not exist, Alice creates it.** Feed your build/release identifier here and each release gets its own assessment record. |

Returns `{ assessmentId }`.

### Re-run an existing assessment

`run-assessment` → `POST /redteam/assessments/run/{id}`

Path param `id` is the assessment identifier. Returns `{ assessmentId }`.

### Clone and run

`clone-and-run-assessment` → `POST /redteam/assessments/cloneAndRun/{id}`

Creates a **new** assessment from an existing one and runs it. Returns the
`assessmentId` of the new clone, not the original.

Query param `reusePrompts` (boolean) is the meaningful control:
- `true` — reuse the original adversarial prompts. Use this for a **regression check**: same
  attacks, new build, comparable results.
- `false` — generate fresh prompts. Use this to **widen coverage** and avoid overfitting to a
  known attack set.

## Poll for completion

`get-assessments` → `GET /redteam/assessments/`

This is the only paginated and filterable operation in the whole API.

**Filters:** `search` (by name), `applicationIds[]`, `applicationNames[]`, `status[]`,
`createdBy[]` (creator emails), `dateFrom` / `dateTo` (ISO 8601).

**Paging:** `page` (min 1), `limit` (min 1, max 100, default 20), `sort`
(`createdAt` | `lastUpdatedAt` | `name` | `status`), `order` (`asc` | `desc`).

**Response:** `{ data: [...], pagination: {...} }`. Each row carries `assessmentId`,
`applicationName`, `versionName`, `name`, `status`, `createdAt`, `lastUpdatedAt`.

### Status lifecycle

`pending` → `in_progress` → `generating_report` → `completed`

with `ready` and `failed` as the other terminal/initial states.

Poll with `applicationNames=<your app>&status=completed&status=failed` and let your gate act
on which terminal state arrives. Note `generating_report` is a distinct state — an assessment
that has finished running is **not** yet readable; wait for `completed`.

## A release gate, end to end

1. `run-assessment-preset` with `version_name` set to your build id → capture `assessmentId`.
2. Poll `get-assessments` filtered by `applicationNames` and sorted `createdAt desc` until
   your `assessmentId` reaches `completed` or `failed`.
3. Fail the build on `failed`; on `completed`, retrieve the report from the Alice console.
4. On the next release, `clone-and-run-assessment` with `reusePrompts=true` against the prior
   assessment to get a like-for-like regression comparison.

## Errors

| Status | Meaning |
|---|---|
| `400` | Validation failed (`get-assessments`, `run-assessment-preset`). Check `params.body.keys`. A `preset_name` or `app_name` that is not configured lands here. |
| `401` | Bad or missing `af-api-key`. |
| `429` | Over 50 req/s — relevant if you poll tightly. Use an interval measured in seconds, not milliseconds. |

The spec declares **no `404`** on `run-assessment` or `clone-and-run-assessment` even though
both take a path `id`. Do not assume an unknown id produces a clean 404 — handle an unexpected
status.

## See also

- `skills/activefence-guard-genai-messages.md` — the runtime half of the lifecycle
- `conventions/activefence-conventions.yml`
- `errors/activefence-problem-types.yml`
