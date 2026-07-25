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

## Timestamps

- **Created:** 2026-07-25
- **Modified:** 2026-07-25

## APIs

None. Evari publishes no public, self-serve API.

Every candidate developer host was probed on 2026-07-25 and none resolved — `developer.`, `developers.`, `docs.` and `api.` across `evari.com`, `evari.insure` and `evari.tech` all fail DNS. On the live corporate site the paths `/developers`, `/api`, `/docs` and `/integrations` return HTTP 200 but serve the homepage byte-for-byte; `robots.txt` disallows `/api/`; `/openapi.json` and `/swagger.json` return 404.

The real API surface exists but is tenant-scoped and closed. The CloudStream application ships a build config naming `https://api.cloudstream.evari.tech/api` and an `/api/docs` path — that host answers HTTP 404 on every path probed. The Envest tenant backend at `https://api.envest.evari.tech` returns HTTP 502. The customer app (`app.evari.insure`) and the admin console (`admin.cloudstream.evari.tech`) are login walls. Authentication is a first-party, unpublished token service (`auth.cloudstream.evari.tech`, client id `app`) that serves no anonymous OIDC discovery.

CloudStream markets quote, bind and issue, but none of the four insurance verbs are exposed programmatically to the public, and there is no FNOL API — claims appear only as AI document-processing of intake forms.

**ACORD posture: no ACORD reference found.** Zero matches for ACORD, AL3 or IVANS across the full site corpus. The agency-management vocabulary present is vendor-integration naming — Vertafore (AMS360, Sagitta), Applied Epic, Socotra, Guidewire (read access) — systems Evari connects *into*. Evari is a consumer of other vendors' APIs, not a publisher of its own.

Note on domains: `evari.com` is a parked "for sale" lander and is not the company. The original `evari.com.au` redirects to `evari.insure`, which now returns 404 everywhere. The live company site is **https://evari.tech**.

See [review.yml](review.yml) for the full probe log, provenance and HTTP statuses.

## Links

- [Website](https://evari.tech/)
- [Help Center](https://evari.tech/help-center/)
- [Blog](https://evari.tech/blog/)
- [Trust Center](https://evari.tech/trust)
- [Security Disclosure](https://evari.tech/.well-known/security.txt)
- [Pricing](https://evari.tech/pricing)
- [LinkedIn](https://www.linkedin.com/company/evari/)
