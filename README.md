# Evari

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

Evari is an insurance technology company founded in Sydney by Daniel Fogarty (former CEO of Zurich Australia and New Zealand), Robert Jeffery and Brack Norris, and now operating as Evari Services UK Ltd. It launched as a digital small-business and trades insurance brand at evari.insure, a Lloyd's coverholder with direct and partner distribution, then moved upstream into core systems with CloudStream, a cloud-native policy administration platform covering quote, bind and issue through endorsement, renewal and cancellation, broker and MGA portals, appetite and eligibility rules, commission tracking and policyholder self-service. Its current positioning is insurance AI operations for brokers, MGAs and insurers, delivered as 30-day assistant deployment sprints powered by the third-party QuivaWorks platform. Evari publishes no developer portal and no API reference, and every running API host is tenant-scoped and closed - api.cloudstream.evari.tech returns 404 unauthenticated, api.envest.evari.tech returns 502, and the customer and admin applications are login walls. One real first-party contract does exist off-portal - Evari published its Quotes microservice to npm as evari-quotes-api, and that tarball ships a generated Swagger 2.0 document of 49 paths and 56 operations plus a draft-07 JSON Schema set of 369 definitions, both harvested here. Evari is otherwise a consumer of other vendors' APIs, integrating into Socotra, Vertafore AMS360 and Sagitta, Applied Epic and Guidewire read access, and no ACORD, AL3 or IVANS reference appears anywhere on its site, in its help centre or in its data model.

**Areas:** Insurance · Australia · Insurtech · Policy Administration · Core Systems · Property and Casualty · Underwriting · Claims · Brokerage · MGA · Artificial Intelligence · Quoting

## Evari on APIs.io

Everything profiled for Evari is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/evari/](https://apis.io/providers/evari/)** — or go straight to one of the APIs or properties below.

### APIs (1)

- [Evari Quotes API](https://apis.io/apis/evari/evari-quotes-api/) — The Evari Quotes microservice - the internal broker and underwriter quoting surface at /api/quotes/** plus a customer-facing mirror at…

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [evari-quotes](https://apis.io/servers/evari/evari-quotes/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Evari Agentic Access](https://apis.io/agentic-access/evari/evari-agentic-access/)

#### JSON Schema (1)

The data models the API reads and writes.

- [Evari Contracts Types](https://apis.io/schemas/evari/evari-contracts-types/)

#### Collections (1)

Postman and Open Collection request collections.

- [Evari Quotes API](https://apis.io/collections/evari/open-evari-quotes-api/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Evari Quotes Api Overlay](https://apis.io/overlays/evari/evari-quotes-api-overlay/)

#### Security (4)

Authentication, trust centre, and vulnerability disclosure.

- [Evari Authentication](https://apis.io/security/evari/evari-authentication/)
- [Evari Domain Security](https://apis.io/security/evari/evari-domain-security/)
- [Evari Trust Center](https://apis.io/security/evari/evari-trust-center/)
- [Evari Vulnerability Disclosure](https://apis.io/security/evari/evari-vulnerability-disclosure/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Evari Plans](https://apis.io/plans/evari/evari-plans/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://evari.tech/)
- [Documentation](https://evari.tech/help-center/)
- [Getting started](https://evari.tech/help-center/categories/getting-started/)
- [Pricing](https://evari.tech/pricing)
- [Sign up](https://quiva.ai/)
- [Support](https://evari.tech/help-center/contact/)
- [Blog](https://evari.tech/blog/)
- [Security](https://evari.tech/.well-known/security.txt)
- [Compliance](https://evari.tech/trust)
- [Trust centre](https://evari.tech/trust)
- [Terms of service](https://evari.tech/legal#terms)
- [Privacy policy](https://evari.tech/legal#privacy)
- [GitHub](https://github.com/myevari)

## API Evangelist rating

**Kin Score 47.6** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 73.2 |
| Contract quality | 43.5 |
| Contract governance | 18.2 |
| Operational transparency | 13.2 |
| Developer ergonomics | 42.3 |
| Access clarity | 78.9 |

**Agent readiness 20.9** — agent-aware

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | — |
| OpenAPI Examples | — |
| Rate Limit Signal | — |
| Event Surface Described | — |
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

**Regulatory alignment 29.5** — Insurance

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/evari/](https://apis.io/providers/evari/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Evari: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/evari/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
