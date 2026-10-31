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
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

ActiveFence — now operating as Alice — is an AI security, safety and trust & safety company headquartered in New York and Tel Aviv. It sells two product families through one REST API at api.alice.io: ActiveFamily (ActiveScore automated detection plus the ActiveOS moderation workbench) for user-generated-content trust and safety across text, image, video and audio in 120+ languages and 20+ abuse areas; and WonderSuite for generative-AI protection — WonderBuild (pre-deployment red teaming and adversarial assessment of models, apps and agents), WonderFence (real-time runtime guardrails that evaluate prompts and responses for prompt injection, jailbreaks, PII leakage and policy violations) and WonderCheck (ongoing post-launch evaluation and drift detection). The API offers synchronous endpoints for low-latency moderation and asynchronous endpoints that acknowledge receipt and post results back to a customer-configured callback URL, plus configurable action webhooks fired from the ActiveOS moderation view or an automated workflow. Authentication is a single af-api-key header issued from the platform console; the default rate limit is 50 requests per second. First-party SDKs ship for Python (wonderfence-sdk) and TypeScript (@alice-io/wonderfence-ts-sdk), with a Parlant integration and the open-source Caterpillar agent-skill security scanner. Alice is SOC 2 and ISO 27001 certified.

**Areas:** AI Safety · AI Security · Trust and Safety · Content Moderation · Guardrails · Red Teaming · LLM Security · Prompt Injection · AI Governance · Risk Scoring · User Generated Content · Child Safety

## ActiveFence on APIs.io

Everything profiled for ActiveFence is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/activefence/](https://apis.io/providers/activefence/)** — or go straight to one of the APIs or properties below.

### APIs (7)

- [ActiveFence api keys API](https://apis.io/apis/activefence/activefence-api-keys-api/) — Provides APIs to manage API key(s), including adding new keys, listing existing keys, and deleting keys.
- [ActiveFence Collection API](https://apis.io/apis/activefence/activefence-collection-api/) — Collection API Represents grouped entities. A collection is comprised of multiple items grouped together in a playlist, album, folder, group or channel on…
- [ActiveFence Content API](https://apis.io/apis/activefence/activefence-content-api/) — Content APIs Represents WHAT content was created on your platform, such as a post, comment, review, message, article or data. For example, a web page…
- [ActiveFence Flags API](https://apis.io/apis/activefence/activefence-flags-api/) — The Flags API enables you to send details about the flag made on an item on your platform to the Alice T&S platform.
- [ActiveFence Users API](https://apis.io/apis/activefence/activefence-users-api/) — Users API Represents WHO created content on your platform. These are the end users that have uploaded content to your platform, meaning the people who are…
- [ActiveFence Wonder Build API](https://apis.io/apis/activefence/activefence-wonderbuild-api/) — WonderBuild provides red teaming and security assessment tools for AI applications. APIs for running comprehensive security assessments on gen-AI applications.
- [ActiveFence Wonder Fence API](https://apis.io/apis/activefence/activefence-wonderfence-api/) — WonderFence provides real-time guardrails for AI-generated content. APIs for evaluating and moderating AI-generated content and interactions to protect…

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Activefence Webhooks](https://apis.io/asyncapis/activefence/activefence-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [activefence-mcp.yml](https://apis.io/servers/activefence/activefence-mcp-yml/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Activefence Agentic Access](https://apis.io/agentic-access/activefence/activefence-agentic-access/)

#### Collections (7)

Postman and Open Collection request collections.

- [Alice API Documentation api keys API](https://apis.io/collections/activefence/open-activefence-api-keys-api/)
- [Alice API Documentation Collection API](https://apis.io/collections/activefence/open-activefence-collection-api/)
- [Alice API Documentation Content API](https://apis.io/collections/activefence/open-activefence-content-api/)
- [Alice API Documentation Flags API](https://apis.io/collections/activefence/open-activefence-flags-api/)
- [Alice API Documentation Users API](https://apis.io/collections/activefence/open-activefence-users-api/)
- [Alice API Documentation Wonder Build API](https://apis.io/collections/activefence/open-activefence-wonderbuild-api/)
- [Alice API Documentation Wonder Fence API](https://apis.io/collections/activefence/open-activefence-wonderfence-api/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Activefence Alice Api Overlay](https://apis.io/overlays/activefence/activefence-alice-api-overlay/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Activefence Authentication](https://apis.io/security/activefence/activefence-authentication/)
- [Activefence Domain Security](https://apis.io/security/activefence/activefence-domain-security/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://alice.io/)
- [Documentation](https://docs.activefence.com/index.html)
- [Getting started](https://docs.activefence.com/index.html#section/Authentication)
- [API reference](https://docs.activefence.com/index.html)
- [Support](https://alice.io/contact-us)
- [Blog](https://alice.io/blog)
- [Terms of service](https://alice.io/terms-of-use)
- [Privacy policy](https://alice.io/privacy-policy)
- [GitHub](https://github.com/ActiveFence)

## API Evangelist rating

**Kin Score 51.7** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 73.2 |
| Contract quality | 60.3 |
| Contract governance | 18.2 |
| Operational transparency | 10.5 |
| Developer ergonomics | 69.6 |
| Access clarity | 35.5 |

**Agent readiness 30.4** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | derived (partial credit) |
| OpenAPI Examples | verified |
| Rate Limit Signal | — |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | partial |
| Operation Distinctiveness | distinct |

**Regulatory alignment 29.4** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/activefence/](https://apis.io/providers/activefence/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for ActiveFence: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/activefence/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
