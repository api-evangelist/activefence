# ActiveFence

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

ActiveFence — now operating as **Alice** — is an AI security, safety and trust & safety company
headquartered in New York and Tel Aviv. It sells two product families through one REST API at
`api.alice.io`:

- **ActiveFamily** — ActiveScore automated detection plus the ActiveOS moderation workbench, for
  user-generated-content trust and safety across text, image, video and audio in 120+ languages
  and 20+ abuse areas.
- **WonderSuite** — generative-AI protection: **WonderBuild** (pre-deployment red teaming),
  **WonderFence** (real-time runtime guardrails for prompts and responses) and **WonderCheck**
  (post-launch evaluation and drift detection).

## What this profile is built from

| Surface | Location | Status |
|---|---|---|
| OpenAPI 3.0.0 (18 operations) | `https://docs.activefence.com/openapi.json` | 200 — harvested verbatim to `openapi/_original/` |
| llms.txt | `https://alice.io/llms.txt` | 200 — saved verbatim to `llms/` |
| Public Postman collection | `https://www.postman.com/activefence-demo-team` | 200 |
| Python SDK | `wonderfence-sdk` on PyPI | first-party |
| TypeScript SDK | `@alice-io/wonderfence-ts-sdk` on npm | first-party |
| CLI | `@alice-io/caterpillar` (agent-skill security scanner) | first-party |
| Certifications | SOC 2 Type II, ISO 27001 | badged on `alice.io`, asserted in `llms.txt` |

**Not published by this provider:** no `/.well-known/` documents on any host, no `security.txt`,
no A2A agent card, no hosted MCP server, no status page, no changelog, no deprecation policy, no
AsyncAPI, and no idempotency contract. Each of those is recorded with the URL probed and the
status it returned — see `well-known/`, `lifecycle/` and `conformance/`.

**Brand transition note:** `www.activefence.com` now redirects to `alice.io`, but the docs host is
still `docs.activefence.com` and the auth header is still `af-api-key`. Integrators should expect
both names across the surface.

- https://alice.io/
- https://docs.activefence.com/index.html
- https://www.hiive.com/securities/activefence-stock
