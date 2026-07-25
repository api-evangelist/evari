---
name: Evari price a mid-term endorsement
description: Apply a mid-term change to a bound Evari policy, read the structured diff of what changed, and price the delta.
api: openapi/evari-quotes-api-openapi.yml
generated: '2026-07-25'
method: generated
source: openapi/evari-quotes-api-openapi.yml
operations:
  - EndorsementGet
  - EndorsementPatch
  - EndorsementGetDiff
  - EndorsementGetPrice
---

# Evari price a mid-term endorsement

An `Endorsement` in Evari is a change against an existing quote/policy that is priced
as a delta. Its distinguishing feature is a **first-class diff model** — you can ask
the API what changed rather than computing it client-side.

## Before you start

- **Auth.** `Authorization` header apiKey.
- An endorsement belongs to a `Quote` (`quote`) and references a `policyId`. You need
  an existing endorsement id; this spec exposes no create-endorsement operation, so
  the endorsement is opened elsewhere in the platform.
- **No idempotency key** — `EndorsementPatch` is the only write here and must not be
  blind-retried.

## Steps

1. **Read the endorsement.** `EndorsementGet` — `GET /api/quotes/endorsements/{id}`.
   Returns an `EndorsementQuoteResponse` carrying the endorsement covers and their
   price components.
2. **Apply the change.** `EndorsementPatch` — `PATCH /api/quotes/endorsements/{id}`
   with an `EndorsementQuoteUpdateRequest`. Answers, covers, limits, interested
   parties and dates are all patchable.
3. **Read the diff.** `EndorsementGetDiff` —
   `GET /api/quotes/endorsements/{id}/diff`. Returns `EndorsementDiffResponse`,
   composed of `AnswerDiff`, `CoverDiff`, `LimitDiff`, `InterestedPartyDiff` and
   `DateDiff`. **Use this as the change record you show the customer and file for
   audit** — it is the API's own account of what moved, so do not reconstruct it by
   comparing snapshots.
4. **Price the delta.** `EndorsementGetPrice` —
   `GET /api/quotes/endorsements/{id}/price`. Read `EndorsementPriceComponent` and
   `EndorsementPriceSummary`; as everywhere in this API, price errors come back as
   data on a 200 response, not as an HTTP error.

## Notes

- Endorsement covers mirror quote covers one-for-one
  (`EndorsementCover` -> `EndorsementCoverPriceComponent` /
  `EndorsementCoverPriceSummary`), so cover-level pricing logic you wrote for quotes
  transfers directly.
- Date changes are constrained by the product's quote-date configuration —
  `QuoteDateConfigGet` on `/api/quotes/products/{id}/quote-date-config` before you
  patch dates.
- See `data-model/evari-data-model.yml` for the full entity graph.
