# Evari (evari)

Evari is an Australian insurance technology company, founded in Sydney by Daniel Fogarty (former CEO of Zurich Australia and New Zealand), Robert Jeffery and Brack Norris. It launched as a digital small-business and trades insurance brand at evari.insure, operating as a Lloyd's coverholder with direct and partner distribution, then moved upstream into core systems with CloudStream, a cloud-native policy administration platform covering quote, bind and issue through endorsement, renewal and cancellation, broker and MGA portals, appetite and eligibility rules, commission tracking and policyholder self-service. Its current positioning is insurance AI operations for brokers, MGAs and insurers, delivered as 30-day assistant deployment sprints powered by the third-party QuivaWorks platform.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/evari/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/evari/refs/heads/main/apis.yml)

## Tags

- Insurance
- Australia
- Insurtech
- Policy Administration
- Core Systems
- Property and Casualty
- Underwriting
- Claims
- Broker
- MGA
- Artificial Intelligence
- Quoting
- Endorsements

## Timestamps

- **Created:** 2026-07-25
- **Modified:** 2026-07-25

## APIs

**One API, harvested off-portal: the Evari Quotes API.**

Evari publishes no developer portal, no API reference and no self-serve access — but it did publish a real, first-party, machine-readable contract, in a place no portal probe would ever look. Evari pushed its own Quotes microservice to the public npm registry as [`evari-quotes-api`](https://www.npmjs.com/package/evari-quotes-api) (author "Evari Insure", maintainer `brack@evari.insure` — co-founder Brack Norris), and the published tarball ships the generated spec:

- **[openapi/evari-quotes-api-openapi.yml](openapi/evari-quotes-api-openapi.yml)** — Swagger 2.0, **49 paths, 56 operations, 70 definitions**, harvested verbatim from `dist/swagger.yaml`.
- **[json-schema/evari-contracts-types.json](json-schema/evari-contracts-types.json)** — JSON Schema draft-07, **369 definitions** from the private `@evari/contracts` package, harvested verbatim from `dist/types.json`.

The spec splits into an internal broker/underwriter surface (`/api/quotes/**`, 38 operations) and a customer-facing mirror (`/api/quotes/public/**`, 18 operations, including two SMS-confirmation operations that exist only there). It covers quote create/read/patch, product questions, validation, pricing, quote options, PDF issue, attachments, mid-term **endorsements with a first-class structured diff model**, and **referral to a human underwriter** with notes and per-cover price overrides. Pricing failure is modelled as data on a 200 response — consistent with the spec documenting **zero 4xx/5xx responses** on any operation. Auth is a single apiKey in the `Authorization` header; no OAuth, no scopes.

The wider 369-definition contract set exposes a full **claims** domain, plus agents, billing and cancellation — entities with no published HTTP surface at all. That is the shape of the closed platform behind the login wall.

### What is still absent

The API is tenant-scoped and closed. Every candidate developer host fails DNS — `developer.`, `developers.`, `docs.` and `api.` across `evari.com`, `evari.insure` and `evari.tech`. On the live corporate site `/developers`, `/api`, `/docs`, `/integrations`, `/changelog` and `/roadmap` all return HTTP 200 serving the homepage byte-for-byte; `robots.txt` disallows `/api/`. The only API root named in a first-party build config, `https://api.cloudstream.evari.tech/api`, answers 404 on every path unauthenticated (so the `baseURL` recorded here is **inferred and unverified**); the Envest tenant backend returns 502. There is no SDK (the one public package is the service itself; the `@evari` npm scope is private), no MCP server of Evari's own, no webhooks or AsyncAPI, no GraphQL, no status page, no changelog, no roadmap and no Postman collection. Account creation is directed to **quiva.ai**, the third-party QuivaWorks platform.

**ACORD posture: no ACORD reference found.** Zero matches for ACORD, AL3 or IVANS across the full site corpus — and now also across all 439 harvested schema definitions. The entity model (Quote, Cover, CoverLimit, InterestedParty, Endorsement, ReferredQuote) is proprietary. The agency-management vocabulary present is vendor-integration naming — Vertafore (AMS360, Sagitta), Applied Epic, Socotra, Guidewire (read access) — systems Evari connects *into*.

Note on domains: `evari.com` is a parked "for sale" lander and is not the company. The original `evari.com.au` redirects to `evari.insure`, which now returns 404 everywhere. The live company site is **https://evari.tech**.

## Artifacts

| Artifact | What it holds |
|---|---|
| [openapi/](openapi/) | Swagger 2.0 for the Quotes API (+ the original JSON) |
| [json-schema/](json-schema/) | 369 draft-07 definitions from `@evari/contracts` |
| [overlays/](overlays/) | API Evangelist overlay — provenance, host binding, tag split, recorded gaps |
| [authentication/](authentication/) | Single apiKey scheme in the `Authorization` header |
| [conventions/](conventions/) | Pagination, PATCH semantics, public/internal split, no idempotency, no error contract |
| [data-model/](data-model/) | Entity graph — Product → Quote → Answer/Cover/InterestedParty → pricing, Endorsement, ReferredQuote |
| [skills/](skills/) | Four agent skills grounded in real operationIds |
| [mcp/](mcp/) | 56 **candidate** tools derived from the spec — Evari ships no MCP server |
| [agentic-access/](agentic-access/) | `x-agentic-access` contracts for all 56 operations |
| [conformance/](conformance/) | ISO 27001 + GDPR published; SOC 2 claimed only in a pricing FAQ; no ACORD |
| [lifecycle/](lifecycle/) | No versioning, no deprecation policy, no status page; retention windows |
| [plans/](plans/) | Sprint pricing (A$12k/18k/35k) + platform tiers (A$2k/4k/8k per month) |
| [packages/](packages/) | The one public npm package; the `@evari` scope is private |
| [well-known/](well-known/) | Real RFC 9116 `security.txt`; every other `/.well-known/` path is a catch-all |
| [security/](security/) | Domain security probe, vulnerability disclosure, trust center |
| [llms/](llms/) | Generated `llms.txt` index for this repository |

See [review.yml](review.yml) for the full probe log, provenance and HTTP statuses.

## Links

- [Website](https://evari.tech/)
- [Help Center](https://evari.tech/help-center/)
- [Blog](https://evari.tech/blog/)
- [Trust Center](https://evari.tech/trust)
- [Security Disclosure](https://evari.tech/.well-known/security.txt)
- [Pricing](https://evari.tech/pricing)
- [Getting Started](https://evari.tech/help-center/categories/getting-started/)
- [Support](https://evari.tech/help-center/contact/)
- [Terms of Service](https://evari.tech/legal#terms)
- [Privacy Policy](https://evari.tech/legal#privacy)
- [GitHub Organization](https://github.com/myevari)
- [npm — evari-quotes-api](https://www.npmjs.com/package/evari-quotes-api)
- [LinkedIn](https://www.linkedin.com/company/evari/)
